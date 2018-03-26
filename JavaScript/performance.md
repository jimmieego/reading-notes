## The Cost of JavaScript
https://medium.com/dev-channel/the-cost-of-javascript-84009f51e99e

**less code = less parse/compile + less transfer + less to decompress

Byte-for-byte, JavaScript is more expensive for the browser to process than the equivalently sized image or Web Font — Tom Dale

There is a 2–5x difference in time to parse/compile code between the fastest phones on the market and average phones.

Removing non-critical JavaScript from your pages can reduce transmission times, CPU-intensive parsing & compiling and potential memory overhead. This also helps get your pages interactive quicker.

Loading code proportionate to what’s in view is the holy grail. PRPL and Progressive Bootstrapping are patterns that can help accomplish this.

Transmission size is critical for low end networks. Parse time is important for CPU bound devices. Keeping these low matters.

If you’re building a site that targets mobile devices, do your best to develop on representative hardware, keep your JavaScript parse/compile times low and adopt a Performance Budget for ensuring your team are able to keep an eye on their JavaScript costs.