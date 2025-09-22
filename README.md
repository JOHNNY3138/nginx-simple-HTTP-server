# nginx-simple-HTTP-server
NGINX can be configured as a simple HTTP server to serve static content like HTML, CSS, JavaScript, and images. Here's a basic configuration example:
1. Install NGINX:
On most Linux distributions, you can install NGINX using your package manager. For example, on Ubuntu:
Code

sudo apt update
sudo apt install nginx
2. Configure NGINX:
The main NGINX configuration file is typically located at /etc/nginx/nginx.conf. You'll also find site-specific configurations in /etc/nginx/sites-available/ and /etc/nginx/sites-enabled/.
Create a new configuration file for your simple server in sites-available, e.g., /etc/nginx/sites-available/myserver:
Code

server {
    listen 80; # Listen on port 80 for HTTP requests
    server_name example.com www.example.com; # Replace with your domain name or IP address

    root /var/www/html; # The directory containing your website files
    index index.html index.htm; # Default files to serve when a directory is requested

    location / {
        try_files $uri $uri/ =404; # Try to serve the requested file, then the directory's index, otherwise return 404
    }
}
Explanation of directives:
listen 80;: Specifies that NGINX should listen for incoming HTTP connections on port 80.
server_name example.com www.example.com;: Defines the domain names that this server block will respond to. You can use your actual domain or an IP address.
root /var/www/html;: Sets the document root, which is the directory where NGINX will look for your website files.
index index.html index.htm;: Specifies the default files NGINX will serve when a request is made for a directory (e.g., if someone visits http://example.com/, it will look for index.html or index.htm in /var/www/html/).
location / { ... }: Defines how NGINX should handle requests for paths starting with /.
try_files $uri $uri/ =404;: This directive attempts to serve the requested URI as a file ($uri), then as a directory ($uri/), and if neither is found, it returns a 404 Not Found error.
3. Enable the Server Block:
Create a symbolic link from your configuration file in sites-available to sites-enabled:
Code

sudo ln -s /etc/nginx/sites-available/myserver /etc/nginx/sites-enabled/
4. Test and Reload NGINX:
Test your NGINX configuration for syntax errors:
Code

sudo nginx -t
If the test is successful, reload NGINX to apply the changes:
Code

sudo systemctl reload nginx
5. Place your website files:
Place your HTML, CSS, JavaScript, and image files in the /var/www/html directory (or the root directory you specified).
Now, when you navigate to your server's IP address or domain name in a web browser, NGINX will serve your static content.
