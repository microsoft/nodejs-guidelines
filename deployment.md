## Deployment
> :triangular_flag_on_post: **TODO**
* Continuous integration with VSO.
* Docker and containers.
* Cross-platform remote debugging.

### Process Management (Keeping Applications Running)

Process managers will function to keep your node-based applications running while keeping some complexity outside of your application's code.  Features vary and may include restart on failure, clustering, and rolling-upgrades.

* [PM2](http://pm2.keymetrics.io/)
* [forever](https://www.npmjs.com/package/forever)
* [node-cluster-service](https://github.com/godaddy/node-cluster-service)
* [nodemon](http://nodemon.io/)

### Deployment on Windows
* Running As A Service
  * [windows-service](https://www.npmjs.com/package/windows-service)
  * [node-windows](https://github.com/coreybutler/node-windows)
  * [Non-Sucking Service Manager (NSSM)](http://nssm.cc/)
  * [WinSer](http://jfromaniello.github.com/winser/) wrapper for NSSM
  * Service Alternative: [Use Task Sheduler to run a task at startup](http://www.howtogeek.com/138159/how-to-enable-programs-and-custom-scripts-to-run-at-boot/)
* [Application Request Routing (ARR)](http://www.iis.net/downloads/microsoft/application-request-routing) for IIS
  * Setup ARR as reverse-proxy to node app running as a service
* iisnode:
  * [GitHub repo](https://github.com/tjanczuk/iisnode/wiki) and [wiki](https://github.com/tjanczuk/iisnode/wiki)
  * [Scott Hanselman's blog post](http://www.hanselman.com/blog/InstallingAndRunningNodejsApplicationsWithinIISOnWindowsAreYouMad.aspx)
