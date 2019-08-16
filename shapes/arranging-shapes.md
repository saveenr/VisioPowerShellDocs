# Format-VisioShape



The `Format-VisioShape` cmdlet allows you to control how shapes are laid out on the page.



### Nudge shapes <a id="nudge-shapes"></a>

```text
# nudge shape 1 inch right
Format-VisioShape -NudgeX 1

# nudge shape 1 inch left
Format-VisioShape -NudgeX -1

# nudge shape 1 inch up
Format-VisioShape -NudgeX 1

# nudge shape 1 inch down
Format-VisioShape -Nudge
```



### Aligning shapes <a id="aligning-shapes"></a>

```text
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



### Distributing shapes along an axis <a id="distributing-shapes-along-an-axis"></a>

```text
# Evenly along the x-axis
Format-VisioShape -DistributeHorizontal 

# Evenly along the y axis
Format-VisioShape -DistributeVertical
```

###  <a id="distributing-shapes-along-an-axis"></a>

###  <a id="nudge-shapes"></a>

