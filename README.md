# workflow-trigger-test

Copy of the chat-service CI triggers. Triggers and the detect-changes logic are copied as-is;
every Arthvit/gs-deployment-workflows call is replaced by a local stub-*.yml that only prints.

Push each scenario separately (triggers are evaluated per push):

1. Code only:    edit src/app.py                          -> expect ci + deploy-config
2. Deploy only:  edit deploy/chat/staging/configmap.yaml  -> expect deploy-config only
3. Both:         edit src/app.py and a deploy/ file       -> expect ci + deploy-config

Note: the copied deploy/chat/*.yaml files are comment-only placeholders, so deploy-config's
detect-changes job runs but skips the configmap/secrets jobs. To see those stub jobs run, add a
real key, e.g. `LOG_LEVEL: "info"` in deploy/chat/staging/configmap.yaml.
