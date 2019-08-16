# Org charts from XML



```text
$xmldoc = @"
<orgchart>
  <shape id="0" name="Akuma" />
  <shape id="1" name="Ryu" parentid="0"/>
  <shape id="2" name="Ken" parentid="0"/>
  <shape id="3" name="Chun-Li" parentid="2"/>
</orgchart>
"@


$filename = "d:\model.xml"
$xmldoc | out-file $filename
$model = Import-VisioModel -Filename $filename
$model | Out-Visio

```

![With Visio 2013 and above the Org Chart stencil gives not quite correct results](../.gitbook/assets/snap00009.png)

```

```

