# coding

## sample
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
