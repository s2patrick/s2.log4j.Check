# s2.log4j.Check
SCOM management pack to monitor for log4j vulnerability

I assume all are aware of the log4j vulnerability. To assist you finding concerned systems I’ve created a SCOM management pack which alerts on each (Windows) system affected. Please find the MP attached, ready for import in your management group with no further configuration (but PowerShell v5) required. The workflow runs within 30min (SpreadInitializationOverInterval; to distribute peak on host servers) once a week.
This is an expensive task leading to high CPU (~50%) for a few seconds. Keep in mind to remove it once your environment is safe – or run it on an even higher schedule (like once a week). On some machines you might see random workflow timeouts, even when there are no issues most of the time.

If you have SCCM you might have related files in the ccmcache directory (even when your system is not vulnerable). However, this is excluded in the workflow. If you have other deployment tools in place, it might be necessary to set an override to the “s2 log4j Check Monitor” using the “ExcludePath” property (RegEx-style (ccmcache|uninstall|Recycle.Bin|anyotherstring)).

The recent version only searches on C:\ and D:\ by default to avoid timeouts on many/large volumes (like on file servers). Consider an override if applications are installed on other volumes.

This MP has been tested in my lab and is running in production at a 1000+ agents environment with no issues. However, please try in your own lab before.
Use at your own risk.

Let me know if there are any questions.

Wish you a happy Christmas, relaxing holidays with your family and a successful and healthy 2022.

Take care, 
Patrick

Credits to Jose Espitia (and others before)
https://www.joseespitia.com/2021/12/15/how-to-detect-the-log4shell-vulnerability-with-powershell/

Updates:

21.12.2021: 
* removed SyncTime
* added SpreadInitializationOverInterval = 1800s

25.01.2022: 
* Updated file hashs based on https://github.com/lunasec-io/lunasec/blob/master/tools/log4shell/constants/vulnerablehashes.go
* Added custom hash integration via overrides
* Increased interval to 604800sec (= 1 week)
* Added logging events
* Changed timeout to 900s
* Added overrideable parameter to search only on defined volumes (C:\ and D:\ by default); if applications are being installed on other drives in your environment you have to define it here.
* Excluded mounted drives ("\\...") independent of defined search volumes.
