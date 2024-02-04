# Create two Namespaces and connect them using veth




1. created two namespace named "ns1" & "ns2"

### sudo ip netns add ns1

### sudo ip netns add ns2

2. created a pair of virtul ethernet device named "veth1" & "veth2"

### sudo ip link add veth1 type veth peer name veth2

3. moved virtual ethernet device into namespace

### sudo ip link set veth1 netns ns1
### sudo ip link set veth2 netns ns2

4.configured ip addresses on virtual ethernet devices

### sudo ip netns exec ns1 ip addr add 10.0.0.1/24 dev veth1
### sudo ip netns exec ns2 ip addr add 10.0.0.2/24 dev veth2

5. activated veth in namespace for communication

### sudo ip netns exec ns1 ip link set dev veth1 up
### sudo ip netns exec ns2 ip link set dev veth2 up

6. checked communication from one namespace to another one

### sudo ip netns exec ns1 ping 10.0.0.2
