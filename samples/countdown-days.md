# Countdown days

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio
New-VisioApplication
$doc = New-VisioDocument

$basic_u = Open-VisioDocument basic_u.vss
$master = Get-VisioMaster "Rectangle" $basic_u

$font = $doc.Fonts["Segoe UI"]
$fontid  = $font.ID

# This is a demo, so get some dates relative to the current date
$date_today = Get-Date
$date_today = $date_today.Date
$lower_date = $date_today.AddDays(-3)
$upper_date = $date_today.AddDays(4)
$date_rtm = $date_today.AddDays(2)

$width = 1.0
$height = 1.0 

# Perform the rendering
$cur_date = $lower_date
$n=0
$y=4

$color_normal = "rgb(250,250,250)"
$color_highlight = "rgb(255,0,0)"
$color_target = "rgb(200,200,200)"

while ($cur_date -le $upper_date)
{
    $ss = New-VisioShapeCells

    $x = ($n*$width) + (1.0 + ($width/2.0))
    $shape = New-VisioShape $master $x,$y 

    $ss.XFormWidth = $width
    $ss.XFormHeight = $height
    $ss.FillForeground = $color_normal
    $ss.CharFont = $fontid
    $ss.CharSize = "14pt"

    $text = Get-Date $cur_date -format "M/d"

    
    if ($cur_date -eq $date_rtm)
    {
        $ss.FillForeground = $color_target        
        $text = $text + "`nTARGET"
    }

    if ($cur_date -eq $date_today)
    {
        $ss.FillForeground = $color_highlight
        $text = $text + "`nTODAY"
    }


    Set-VisioShapeCells $ss

    Set-VisioText $text
    Write-Host $cur_date
    $n = $n +1
    $cur_date = $cur_date.AddDays(1)

}
```

