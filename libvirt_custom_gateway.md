<network connections="2">
  <name>remnux_net</name>
  <uuid>34f937f3-fcac-407a-a318-9f076d109702</uuid>
  <bridge name="virbr4" stp="on" delay="0"/>
  <mac address="52:54:00:ec:b8:b7"/>
  <domain name="remnux_net"/>
   <dns>
    <forwarder addr="192.168.100.156"/>
   </dns>
  <ip address="192.168.100.156" netmask="255.255.255.0">
    <dhcp>
      <range start="192.168.100.128" end="192.168.100.254"/>
      <host mac="52:54:00:1e:ac:0a" ip="192.168.100.156"/>
    </dhcp>
  </ip>
</network>
