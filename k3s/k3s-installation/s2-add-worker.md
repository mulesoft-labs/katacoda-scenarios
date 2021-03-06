# Add a worker to the cluster

That was pretty easy, let's add another worker to this cluster by running the agent.

To add the host as an agent to the cluster, we need two things:

* The IP address or DNS name of the server (in this case, the IP address of the host with hostname `master`)
* A cluster secret to join the cluster (in this case, pre-configured for demo purposes)

Run the following command on `node01` to add the host to the cluster:

`echo 'curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.0.1 K3S_CLUSTER_SECRET=thisisverysecret K3S_URL=https://[[HOST_IP]]:6443 sh -' | ssh node01`{{execute T1}}

Wait for node1 to become `Ready` in the cluster by retrieving the nodes in the cluster:

`k3s kubectl get node`{{execute T2}}

For your convenience, the following command will wait until the node shows up as `Ready`:

`until k3s kubectl get node | grep node01 | grep -q ' Ready'; do sleep 1; done; k3s kubectl get node`{{execute T2}}