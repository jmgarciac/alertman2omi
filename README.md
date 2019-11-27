# Alertmanager to HP Omi


 - Settings are in settings.ini. This is where you set the URL where it should inject the OMI alerts
 - Template is in template.xml. It uses jinja.
 - You can run this app inside of openshift with oc new-app.

oc create ns alertman2omi
oc -n alertman2omi delete all -l app=omireceiver
oc -n alertman2omi new-app https://github.com/jmgarciac/alertman2omi.git --context-dir=omireceiver/app --name omireceiver
oc -n alertman2omi delete all -l app=alertman2omi
oc -n alertman2omi new-app https://github.com/jmgarciac/alertman2omi.git --context-dir=app --name alert2omi \
-e OMI_URL="http://omireceiver.alertman2omi.svc:8080/post" \
-e OMI_CATEGORY="INCIDENT"\
-e OMI_CI="OpenShift_POC"


