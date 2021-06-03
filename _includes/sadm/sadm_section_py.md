<a name="sadmin_shell_section"></a>

```python
# ---------------------------------------------------------------------------------------
# SADMIN CODE SECTION 1.49
# Setup for Global Variables and import SADMIN Python module
# To use SADMIN tools, this section MUST be present near the top of your code.    
# ---------------------------------------------------------------------------------------
def setup_sadmin():

    # Load SADMIN Standard Python Library Module ($SADMIN/lib/sadmlib_std.py).
    try :
        SADM = os.environ.get('SADMIN')                                 # Getting SADMIN Root Dir.
        sys.path.insert(0,os.path.join(SADM,'lib'))                     # Add SADMIN to sys.path
        import sadmlib_std as sadm                                      # Import SADMIN Python Libr.
    except ImportError as e:                                            # If Error importing SADMIN 
        print ("Error Importing SADMIN Module: %s " % e)                # Advise User of Error
        sys.exit(1)                                                     # Go Back to O/S with Error
    
    # Create [S]ADMIN [T]ools instance (Setup Dir.,Var.)
    st = sadm.sadmtools()                       

    # You can use variable below BUT DON'T CHANGE THEM - They are used by SADMIN Module.
    st.pn               = os.path.basename(sys.argv[0])                 # Script name with extension
    st.inst             = os.path.basename(sys.argv[0]).split('.')[0]   # Script name without Ext
    st.tpid             = str(os.getpid())                              # Get Current Process ID.
    st.exit_code        = 0                                             # Script Exit Code (Use it)
    st.hostname         = socket.gethostname().split('.')[0]            # Get current hostname

    # CHANGE THESE VARIABLES TO YOUR NEEDS - They influence execution of SADMIN standard library.    
    st.ver              = "2.1"                 # Current Script Version
    st.pdesc            = "Type short description v%s" % st.ver  # Short description of script
    st.log_type         = 'B'                   # Output goes to [S]creen to [L]ogFile or [B]oth
    st.log_append       = False                 # Append Existing Log(True) or Create New One(False)
    st.log_header       = True                  # Show/Generate Header in script log (.log)
    st.log_footer       = True                  # Show/Generate Footer in script log (.log)
    st.multiple_exec    = "N"                   # Allow running multiple copy at same time ?
    st.use_rch          = True                  # Generate entry in Result Code History (.rch) 
    st.debug            = 0                     # Increase Verbose from 0 to 9 
    st.usedb            = True                  # Open/Use Database(True) or Don't Need DB(False)
    st.dbsilent         = False                 # When DB Error, False=ShowErrMsg and True=NoErrMsg 
                                                # But Error Code always returned (0=ok else error)

    # Override Default define in $SADMIN/cfg/sadmin.cfg
    #st.cfg_alert_type   = 1                    # 0=NoMail 1=OnlyOnError 2=OnlyOnSuccess 3=Always
    #st.cfg_alert_group  = "default"            # Valid Alert Group are defined in alert_group.cfg
    #st.cfg_mail_addr    = ""                   # This Override Default Email Address in sadmin.cfg
    #st.cfg_cie_name     = ""                   # This Override Company Name specify in sadmin.cfg
    #st.cfg_max_logline  = 500                  # When Script End Trim log file to 500 Lines
    #st.cfg_max_rchline  = 35                   # When Script End Trim rch file to 35 Lines
    #st.ssh_cmd = "%s -qnp %s " % (st.ssh,st.cfg_ssh_port) # SSH Command to Access Server 

    # Start SADMIN Tools - Initialize 
    st.start()                                  # Init. SADMIN Env. (Create dir.,Log,RCH, Open DB..)
    return(st)                                  # Return Instance Object To Caller
```
