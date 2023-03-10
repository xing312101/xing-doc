# coding

## sample
### MBO
```
## Wo.java
package com.app.workorder;

import java.rmi.RemoteException;
import psdi.mbo.MboSet;
import psdi.util.MXException;

public class Wo extends psdi.pluss.app.workorder.PlusSWO {

  public Wo(MboSet arg0) throws MXException, RemoteException {
    super(arg0);
  }

  public void init() throws MXException{
    System.out.println("WO init()");
    super.init();
  }

}
```
### MBOSET
```
## WoSet.java
package com.app.workorder;

import java.rmi.RemoteException;

import psdi.mbo.Mbo;
import psdi.mbo.MboServerInterface;
import psdi.mbo.MboSet;
import psdi.util.MXException;
import psdi.util.logging.MXLogger;
import psdi.util.logging.MXLoggerFactory;

public class WoSet extends psdi.pluss.app.workorder.PlusSWOSet {

  MXLogger myLogger = MXLoggerFactory.getLogger("maximo.sql.LOCATION.LOCATIONS");

  public WoSet(MboServerInterface arg0) throws MXException, RemoteException {
    super(arg0);
    //TODO Auto-generated constructor stub
  }

  protected Mbo getMboInstance(MboSet ms) throws MXException,RemoteException{
    return new Wo(ms);
  }

}
```

### SERVICE
```
## WoService.java
package com.app.workorder;

import com.app.ComAppUtil;
import java.rmi.RemoteException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.List;

import javax.jws.WebMethod;

import com.ibm.json.java.JSONObject;
import com.ibm.json.java.JSON;
import com.ibm.json.java.JSONArray;

import psdi.app.workorder.WOService;
import psdi.iface.webservices.action.WSMboKey;
import psdi.mbo.MboRemote;
import psdi.mbo.MboSetRemote;
import psdi.server.MXServer;
import psdi.util.MXException;

public class WoService extends WOService {

  private ConnectionKey conKey;
  private DBShortcut dbs;

  public WoService(MXServer mxServer) throws RemoteException {
    super(mxServer);

    try {
      conKey = mxServer.getSystemUserInfo().getConnectionKey();
    } catch (MXException e) {
      e.printStackTrace();
    }
  }

  @WebMethod
  public String updateByPost(@WSMboKey(value = "WORKORDER") MboRemote wo, String data, String version) {
    JSONObject jsonReturnObj = new JSONObject();
    jsonReturnObj.put("success", true);
    return (jsonReturnObj.toString());
  }

  @WebMethod
  public String getDate() {
    JSONArray jsonArray = new JSONArray();
    try {
      dbs = new DBShortcut();
      dbs.connect(conKey);
      StringBuffer sql = new StringBuffer();
      sql.append("select * ");
      sql.append(" from ....");

      ResultSet rs = dbs.executeQuery(sql.toString());

      while (rs.next()) {
        JSONObject jsonObj = new JSONObject();
        jsonObj.put("AAA", rs.getString("AAA"));

        jsonArray.add(jsonObj);
      }

      rs.close();
    } catch (Exception ex) {
      ex.printStackTrace();
      dbs.close();
    } finally {
      dbs.close();
      dbs = null;
    }

    return (jsonArray.toString());
  }
}

```