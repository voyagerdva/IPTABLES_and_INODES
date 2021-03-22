
I. Please write iptables rules that will block all incoming traffic and allow outgoing (browsing from local machine should work, but all incoming connections should be dropped).

    how to do:
    1)	Setting up policies for dropping all incoming and forwarding packets:
        sudo iptables -P INPUT DROP
        sudo iptables -P FORWARD DROP

    2)	Setting up rules for accepting outgoing packets:
        sudo iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
        sudo iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT

    3) After that steps we have the next condition of firewall:
        # iptables -L
        Chain INPUT (policy DROP)
        target     prot opt source               destination
        ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED

        Chain FORWARD (policy DROP)
        target     prot opt source               destination
        ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED

        Chain OUTPUT (policy ACCEPT)
        target     prot opt source               destination



II. There is a directory with 2 files that are shown as '???' and '???'. They have different names, but in console are shown as 3 question marks. How to remove them?

    Perhaps it happened because something wrong to the encoding. The best way to remove that files is to use their inodes. For example:
    # ls -il
    # 17486817 -rw-r--r--. 1 root root 0 Mar 19 12:32 ???
    # 17486837 -rw-r--r--. 1 root root 0 Mar 19 12:32 ???
    # for inod in 17486817 17486837; do find . -inum $inod -delete; done
