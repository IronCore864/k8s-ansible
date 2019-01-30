# Software Infrastructure Inventories

Keeping different teams' inventories in sync didn't work very well,
so now  we created a dedicated set of inventories to be used
by the components of the Software Infrastructure.

### Important points:
1. These inventories are **incomplete**.
Correct/add variables and hosts as needed. **Keep them up-to-date**.

2. Try to **move all variables** into `group_vars/all.yaml`.
This means, introduce new variables on there, and move the existing as you touch them.
The motivation of doing this is to be able to see the whoe cluster configuration in 1 file,
instead of files scattered around.

3. **Name your variables good**: Use long names, prefixes etc. as needed.
Good thing is, the variable files are not simply key-value sets, but YAMLs,
so we can express detailed configurations using YAML model.
Assume that our inventories can be merged by other teams' inventories at any time,
so we should try to avoid collisions/ambiguity in variable names.

4. **Do not put other teams' variables here**:
Every piece of information in these inventories should be used by at least 1 playbook of the
SW Infrastructure.
Example: We keep only `ceph-mon` and `ceph-admin` hosts, because we install the CEPH provisioner
and we need this info. But not the other variables from the HW team. So we keep only these two.

5. **Make sure you do not add anything sensitive here**:
No passwords, no private keys, no secrets.
Look for alternative solutions if you have such use case.

6. **When changing something, think about all playbooks**, and possibility of breaking something:
Try to avoid redundant variables, but also try to avoid reusing something
that actually shouldn't be reused.
