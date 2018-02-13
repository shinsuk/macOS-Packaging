# macOS-Packaging

## Packaging


## Code Signing
On macOS Sierra and later, spctl can be used to assess a disk image's signature, like this:

    $ spctl -a -t open --context context:primary-signature -v MyImage.dmg
    /Users/me/Downloads/MyImage.dmg: accepted
    source=Developer ID

## DMG
    $ hdiutil create -volname [volume name] -srcfolder [source folder] -format UDZO -fs ExFAT -ov [image filename]
    $ hdiutil verify [image filename]

## Install & Uninstall

### Uninstall
    $ pkgutil --pkgs # list all installed packages
    $ pkgutil --files the-package-name.pkg # list installed files

    $ pkgutil --pkg-info the-package-name.pkg # check the location
    $ cd / # assuming the package is rooted at /...
    $ pkgutil --only-files --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -i
    $ pkgutil --only-dirs --files the-package-name.pkg | tr '\n' '\0' | xargs -n 1 -0 sudo rm -ir
    
    $ sudo pkgutil --forget the-package-name.pkg
    
## References

### Packaging
* [Making OS X Installer Packages like a Pro - Xcode Developer ID ready pkg@StackOverflow](https://stackoverflow.com/questions/11487596/making-os-x-installer-packages-like-a-pro-xcode-developer-id-ready-pkg/11487658#11487658)
* [Packaging guidelines for macOS](https://themacwrangler.wordpress.com/2017/04/28/packaging-guidelines-for-mac-os/)
  * [Packages](http://s.sudre.free.fr/Software/Packages/about.html)
    * [Packages User Guide](http://s.sudre.free.fr/Software/documentation/Packages/en_2017/index.html)
* [OS X: Creating Packages from the Command Line - Tutorial and a Makefile - Part I](http://thegreyblog.blogspot.kr/2014/06/os-x-creating-packages-from-command_2.html)
  * [OS X: Creating Packages from the Command Line - Tutorial and a Makefile - Part II](http://thegreyblog.blogspot.kr/2014/06/os-x-creating-packages-from-command.html)
* [OSX flat packages](http://matthew-brett.github.io/docosx/flat_packages.html)
* [Distribution Definition XML Schema Reference@Apple](https://developer.apple.com/library/content/documentation/DeveloperTools/Reference/DistributionDefinitionRef/Chapters/Introduction.html)
    
### Code Signing
* [Technical Note TN2206 macOS Code Signing In Depth@Apple](https://developer.apple.com/library/content/technotes/tn2206/_index.html)
* [Code Signing Requirement Language@Apple](https://developer.apple.com/library/content/documentation/Security/Conceptual/CodeSigningGuide/RequirementLang/RequirementLang.html)

### Install & Uninstall
* [How do I uninstall any Apple pkg Package file?@SuperUser](https://superuser.com/questions/36567/how-do-i-uninstall-any-apple-pkg-package-file)
  * [Uninstalling packages (.pkg files) on Mac OS X](https://wincent.com/wiki/Uninstalling_packages_(.pkg_files)_on_Mac_OS_X)
