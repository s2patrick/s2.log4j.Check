# s2.log4j.Check
SCOM management pack to monitor for log4j vulnerability

I assume all are aware of the log4j vulnerability. To assist you finding concerned systems I’ve created a SCOM management pack which alerts on each (Windows) system affected. Please find the MP attached, ready for import in your management group with no further configuration required. The workflow runs every 24h at 03:30am.
This is an expensive task leading to high CPU (~50%) for a few seconds. Keep in mind to remove it once your environment is safe – or run it on an even higher schedule (like once a week). On some machines you might see random workflow timeouts, even when there are no issues most of the time.

If you have SCCM you might have related files in the ccmcache directory (even when your system is not vulnerable). However, this is excluded in the workflow. If you have other deployment tools in place, it might be necessary to set an override to the “s2 log4j Check Monitor” using the “ExcludePath” property (RegEx-style (ccmcache|uninstall|Recycle.Bin|anyotherstring)).

This MP has been tested in my lab and is running in production at a 1000+ agents environment with no issues. However, please try in your own lab before.
Use at your own risk.

Let me know if there are any questions.

Wish you a happy Christmas, relaxing holidays with your family and a successful and healthy 2022.

Take care, 
Patrick
