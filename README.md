# ExistenceOfDirectory
To check for the existence of a folder on a windows platform
```
proc directory_exists(path)
{
        // The following are defined in Windows header files
        vars FILE_ATTRIBUTE_DIRECTORY = 0x10
        vars INVALID_FILE_ATTRIBUTES = -1
        vars attr, err

        /* There's no need to load kernel32.dll. Its always loaded.
          * A failure to load it probably means you're not running in Windows.
          * Note that even the 64-bit version of it is called kernel32.dll.
          */
        err = sm_slib_load("kernel32.dll")
        if (err != 0)
        {
                msg emsg "kernel32.dll is not loaded"
                return 0
        }
        err = sm_slib_install("GetFileAttributesA(s)", SLIB_C, SLIB_INTFNC)
        if (err != 0)
        {
                msg emsg "Cannot find GetFileAttributesA()."
                return 0
        }
        attr = GetFileAttributesA(path)
        if (attr == INVALID_FILE_ATTRIBUTES)
        {
                return 0
        }
        return ((attr & FILE_ATTRIBUTE_DIRECTORY) == FILE_ATTRIBUTE_DIRECTORY)
}
```
Need a Panther Web 552 Redhat Image? [Click Here](https://hub.docker.com/r/prolificspanther/pantherweb "Named link title") 

[Click Here](https://prolifics.com/panther-trial-license-request/ "Named link title") for a 45-day license.

How to set up a Panther Servlet Web Application? [Click Here](https://github.com/ProlificsPanther/PantherWeb/releases "Named link title")

Read our Documentation [here](https://docs.prolifics.com)
