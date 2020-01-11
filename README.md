# Sverd
This tool installs Debian 10 servers on [Vultr.com](https://vultr.com) with Nginx, node, npm, letsencrypt, zsh, firewall (ufw), mongodb, and waveorb.

Static files are handled by Nginx, which has support for asset caching, brotli compression, https and http2. All processes are handled by `systemd`.

You also get scripts to manage deployment of apps and server updates.

### Configuration
Create a file called sverd.json in your app directory. Add you SSH public key to your Vultr account and replace the `ssh` field with your ssh script id.

Finally, replace `api` in the config file with your Vultr API key.
```javascript
{
  "domain": "waveorb.com",
  "label": "waveorb",
  "hostname": "waveorb",
  "api": "VULTR_API_KEY",
  "os": 352,
  "region": 7,
  "plan": 201,
  "ssh": "5ba4f7cab05d7",
  "env": {
    "names": "waveorb.com www.waveorb.com",
    "exec": "/var/www/server-linux",
    "cert": "/etc/letsencrypt/live/waveorb.com/fullchain.pem",
    "key": "/etc/letsencrypt/live/waveorb.com/privkey.pem",
    "email": "hello@waveorb.com",
    "domains": [
      "waveorb.com",
      "www.waveorb.com"
    ]
  }
}
```

### Usage
After running the `create` script, the IP address of your server will be stored in your `sverd.json` config file.
```bash
# Create server on Vultr
sverd create

# Install software
sverd install

# Update server
sverd update

# Deploy app
sverd deploy
```

ISC licensed. Enjoy!