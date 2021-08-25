
# JMX expose

  If you expose jmx metrics from jvm in the pod , there is an option is to forward JMX port from OCP to your local machine with **port-forward** .

**First add below jvm options to your app:**

```al
-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.local.only=false -Dcom.sun.management.jmxremote.port=1099 -Dcom.sun.management.jmxremote.rmi.port=1099 -Djava.rmi.server.hostname=127.0.0.1
```
:::image type="content" source="jvmoption.jpg" alt-text="":::


Since we can only forward one port,  jmxremote.port and jmxremote.rmi.port should be same. 

**rollout your application**

```bash
oc rollout latest dc/<your-app-name>
oc rollout latest dc/acme
```


**Forward jmx port to your local PC with oc port-forward command:**
```al
oc port-forward <your-app-pod> 1099
oc port-forward acme-sfdfsdf 1099
```
**Open jconsole connection to your local port 1099**

Make sure you have an installed java on your local PC and X window forwarding works properly.

```bash
jconsole 127.0.0.1:1099
```

:::image type="content" source="jconsole.jpg" alt-text=",":::


