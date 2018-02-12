---
title : Visit Jupyter Notebook Within LAN - Windows Version
---

# Run on the server to find out how much jupyter notebook's server IP
ipconfig /all

# Configure jupyter notebook
jupyter notebook --generate-config
echo "c.ConnectionFileMixin.ip = '0.0.0.0'" >> ~ / .jupyter / jupyter_notebook_config.py # All 0 means to accept any IP address access (based on the assumption of trust LAN users)
echo "c.NotebookApp.ip = '0.0.0.0'" >> ~ / .jupyter / jupyter_notebook_config.py
jupyter notebook

# Execute the above command will see the http: //0.0.0:8888/? Token = xxxxxxx tips terminal
# Open the browser, paste the address, the 0.0.0.0 replaced by the server's IP address can be.
