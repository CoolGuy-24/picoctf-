# Forbidden Paths

In this challenge, the flag was stored in `flag.txt`. The challenge description also mentioned two more things. One was that website files live in `/usr/share/nginx/html/`.
Another was that the website was filtering absolute file paths. 

So all I had to do was find a way to access the flag file (which I know is stored in `/usr/share/nginx/html/`) using an indirect path.
Reading up on the syntax of `/usr/share/nginx/html/`, I realised that they were total 3 directories. 

The first one was `/usr/share/` which stores read only files. The second one was `nginx`. This stores files specific to the NGINX server which is an open source web server neeeded for reverse proxy, load balancing and caching.
The last one was `html`which is a default directory for serving web content in NGINX.

So using my knowledge about file systems from linux, I knew I had to go up 3 directories, and I did that by using a relative pathway,
`../../../flag.txt`

This then gave me the flag which was:
`FLAG: picoCTF{7h3_p47h_70_5ucc355_e5fe3d4d}`
