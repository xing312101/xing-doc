# Birt in Maximo


## initail code
```
importPackage(Packages.com.ibm.tivoli.maximo.report.script);

mxReportScriptContext = MXReportScriptContext.initialize(reportContext);

mxReportScriptContext.setDefaultLogLevel("DEBUG");
//mxReportScriptContext.setDefaultLogFile("/File/Path");
scriptLogger = mxReportScriptContext.getReportScriptLogger();
```

## open code
```
dataSet = MXReportDataSetProvider.create(this.getDataSource().getName(), this.getName());
dataSet.open();
dataSet.setQuery(sqlText);
```

## fetch code
```
if (!dataSet.fetch())
	return (false);

row["hello"] = VehicleStatisticsSet.getString("world");

return (true);
```

## console log
```
Packages.java.lang.System.out.println ("this.queryText: " + this.queryText);
```