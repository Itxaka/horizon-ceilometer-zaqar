# horizon-ceilometer-zaqar

Streaming interface for realtime Horizon tables updates

## How to test

1. Spin up an Ubuntu 14.04 LTS instance
2. Install Devstack on it docs.openstack.org/developer/devstack/
3. Add Ceilometer and Zaqar to the local.conf
4. Install MongoDB https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
5. Apply the patch to Horizon 0001-Add-websocket-client-for-tables-updates.patch (git am --signoff < *.patch)
6. Update the credentials (token, project_id) in /opt/stack/horizon/horizon/static/horizon/js/horizon.realtime.js. 
7. Disable JS compress adding COMPRESS_ENABLED = False in local_settings.py under /opt/stack/horizon/openstack_dashboard/local
8. Install and collect static files (pip install -e . and ./manage.py collectstatic under /opt/stack/horizon)
9. Apply the patch to Ceilometer 0001-Add-Zaqar-Publisher.patch (git am --signoff < *.patch)
10. Update the credentials (user, pass, project_id) in /opt/stack/ceilometer/ceilometer/publishers/zaqar.py
11. Copy the pipeline.yaml file under /etc/ceilometer
12. Restart ceilometer-anotification service (screen -r stack, navigate until finding the tab, ctrl+a esc, ctrl+c, run last command)
13. Ready to test with Firebug under Firefox! https://addons.mozilla.org/en-US/firefox/addon/firebug/
