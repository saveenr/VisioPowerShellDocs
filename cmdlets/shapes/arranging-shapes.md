# Format-VisioShape



The `Format-VisioShape` cmdlet allows you to control how shapes are laid out on the page.



### Nudge shapes <a href="#nudge-shapes" id="nudge-shapes"></a>

```
# nudge shape 1 inch right
Format-VisioShape -NudgeX 1

# nudge shape 1 inch left
Format-VisioShape -NudgeX -1

# nudge shape 1 inch up
Format-VisioShape -NudgeX 1

# nudge shape 1 inch down
Format-VisioShape -Nudge
```



### Aligning shapes <a href="#aligning-shapes" id="aligning-shapes"></a>

```
# Align shapes vertically
Format-VisioShape -AlignVertical Top
Format-VisioShape -AlignVertical Center
Format-VisioShape -AlignVertical Bottom

# Align shapes horizontally
Format-VisioShape -AlignHorizontal Left
Format-VisioShape -AlignHorizontal Center
Format-VisioShape -AlignHorizontal Right

# Align shapes horizontally and vertically at the same time
Format-VisioShape -AlignHorizontal Left -AlignVertical Bottom
```



### Distributing shapes along an axis <a href="#distributing-shapes-along-an-axis" id="distributing-shapes-along-an-axis"></a>

```
# Evenly along the x-axis
Format-VisioShape -DistributeHorizontal 

# Evenly along the y axis
Format-VisioShape -DistributeVertical
```

### &#x20;<a href="#distributing-shapes-along-an-axis" id="distributing-shapes-along-an-axis"></a>

### &#x20;<a href="#nudge-shapes" id="nudge-shapes"></a>
