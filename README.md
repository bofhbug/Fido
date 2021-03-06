Fido: Full ISO Download Script (for Windows retail ISOs)
========================================================

[![Licence](https://img.shields.io/badge/license-GPLv3-blue.svg?style=flat-square)](https://www.gnu.org/licenses/gpl-3.0.en.html)
[![Github stats](https://img.shields.io/github/downloads/pbatard/Fido/total.svg?style=flat-square)](https://github.com/pbatard/Fido/releases)

Description
-----------

Fido is a PowerShell script that is primarily designed to be used in [Rufus](https://github.com/pbatard/rufus) but that
can also be used in standalone fashion, and that automates access to the official Windows retail ISO download links.

We decided to create this script because, while Microsoft does make retail ISO download links freely and publicly
available on their website (at least for Windows 8 and Windows 10), it only does so after actively forcing users to
jump through a lot of unwarranted hoops, that create an exceedingly counterproductive, if not downright unfriendly,
consumer experience, which greatly detracts from what people really want (direct access to ISO downloads).

As to the reason one might want to download Windows __retail__ ISOs, as opposed to the ISOs that can be generated by
Microsoft's own Media Creation Tool (MCT), this is because it is only with an official retail ISO that one can assert
with complete certainty whether its content has been altered in any way or not. Indeed, retail Microsoft's ISOs are the
only ones you will be able to obtain an official SHA-1 for (from sites [such as this one](https://msdn.rg-adguard.net/public.php))
allowing you to be 100% certain that the image you are using is non corrupted and safe to use.

This, in turn, offers assurance that the content __YOU__ are using to install your OS, and which it is indeed critical
to validate beforehand if you care about security, does matches bit for bit the one that Microsoft officially released.

On the other hand, because no two MCT ISOs are the same (due to MCT always regenerating the ISO content on the fly)
it is impossible to get the same kind of assurance from non-retail ISOs. Hence the need to provide users with a much
easier and less restrictive way to access official retail ISOs...

License
-------

[GNU General Public License version 3.0](https://www.gnu.org/licenses/gpl-3.0) or later.

How it works
------------

The script basically performs the same operation as one might perform when visiting either of the following URLs (that
is, provided that you have also changed your `User-Agent` browser string, since, when they detect that you are using a
version of Windows that is the same as the one you are trying to download, the Microsoft web servers at these addresses
redirect you __away__ from the pages that allow you to download retail ISOs):

* https://www.microsoft.com/software-download/Windows8ISO
* https://www.microsoft.com/software-download/Windows10ISO

After visiting those with a full browser (Internet Explorer, running through the `Invoke-WebRequest` PowerShell Cmdlet),
to confirm that they are accessible queries web APIs on the Microsoft servers to first request the language selection
available for the for the version of Windows that was selected, and then the download links for the various architecture
enabled for that version + language combination.

Requirements
------------

PowerShell 3.0 or later is required. But the script does detect if you are using an older version and points you to the
relevant PowerShell 3.0 download page if needed, which should only be the case if you are running a vanilla version of
Windows 7.

Also, because Internet Explorer is being used behind the scenes, if you haven't gone through the first time setup for
Internet Explorer, you may receive an error about it when running the script. If that is the case, then you need to
make sure that you manually launch IE at least once and complete the setup.

Note that, if running this script elevated, this annoyance can be avoided by using the `-DisableFirstRunCustomize`
option (which basically __temporarily__ creates the key of the same name in the registry __if__ it doesn't already
exist, to bypass that behaviour).

Additional Notes
----------------

Because of it's intended usage with Rufus, this script is not designed to cover all possible retail ISO downloads, but
mostly those that the general public are likely to use. For instance, we currently have no plan to add support for
LTSB/LTSC Windows 10 ISOs downloads.

If you are interested in such downloads, you are kindly invited to visit the relevant download pages from Microsoft
such as [this one](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise) for LTSC versions.
