https://github.com/cilium/cilium-cli/issues/946

cilium config set enable-local-redirect-policy true

cilium config set enable-local-redirect-policy true
all agents are restarted but fail to start "waiting for all CRDs" indefinitely
restarting cilium-operator fixes the issue by creating the ciliumlocalredirectpolicies.cilium.io CRD.