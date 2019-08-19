# Sample Directed Graph XML 3



```text
$xmldoc = @"
<directedgraph>
  <renderoptions
    usedynamicconnectors="false"
    scalingfactor="20" />
  <shapes>
    <shape id="n1" label="8761|Gus" stencil="basflo_u.vss" master="Process" />
    <shape id="n2" label="0|ProABCS" stencil="basflo_u.vss" master="Predefined process" />
    <shape id="n3" label="ABCS" stencil="basflo_u.vss" master="Stored data" />
    <shape id="n4" label="Global Underwriting" stencil="basflo_u.vss" master="Stored data" />
  </shapes>

  <connectors>
    <connector id="c1"  from="n1" to="n2" label="1111" />
    <connector id="c2" from="n2" to="n3" label="222222" />
    <connector id="c3" from="n4" to="n2" label="3333333" />
  </connectors>

  </page>

  <page>

    <renderoptions
      usedynamicconnectors="true"
      scalingfactor="20"
    />
    <shapes>
      <shape id="n1" label="A" stencil="basflo_u.vss" master="Process" />
      <shape id="n2" label="B" stencil="basflo_u.vss" master="Predefined process" />
      <shape id="n3" label="C" stencil="basflo_u.vss" master="Stored data" />
      <shape id="n4" label="D" stencil="basflo_u.vss" master="Stored data" />
    </shapes>

    <connectors>
      <connector id="c1"  from="n1" to="n2" label="" />
      <connector id="c2" from="n2" to="n3" label="" />
      <connector id="c3" from="n4" to="n2" label="" />
    </connectors>

  </page>
</directedgraph>
"@

$filename = "d:\model.xml"
$xmldoc | out-file $filename
$model = Import-VisioModel -Filename $filename
$model | Out-VisioApplication
```

