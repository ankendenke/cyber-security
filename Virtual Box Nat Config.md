In NAT mode, the guest network interface is assigned to the IPv4 range ``10.0._`x`_.0/24`` by default where _`x`_ corresponds to the instance of the NAT interface +2. So _`x`_ is 2 when there is only one NAT instance active. In that case the guest is assigned to the address `10.0.2.15`, the gateway is set to `10.0.2.2` and the name server can be found at `10.0.2.3`.

If the NAT network needs to be changed, use the following command:
```
$ VBoxManage modifyvm _`VM-name`_ \
--natnet1 "192.168/16"
```
This command would reserve the network addresses from `192.168.0.0` to `192.168.254.254` for the first NAT network instance of _`VM-name`_ The guest IP would be assigned to `192.168.0.15` and the default gateway could be found at `192.168.0.2`.

Source: https://www.virtualbox.org/manual/ch09.html#changenat
