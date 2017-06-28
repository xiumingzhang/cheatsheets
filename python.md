### Insert lines to file

```
f = open(mtlFile, 'r')
lines = f.readlines()
f.close()
insertAt = 5
lines.insert(insertAt, newLine)
f = open(mtlFile, 'w')
lines = ''.join(lines) # list to string
f.write(lines)
f.close()
```


### Visualize matrix (single plot, colorbar matches image height, save without display, tight margins, resolution)

```
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
from mpl_toolkits.axes_grid1 import make_axes_locatable

plt.figure(figsize=(14, 14)); ax = plt.gca()
img = ax.imshow(r)
# Create an axes on the right side of ax. The width of cax will be 2%
# of ax and the padding between cax and ax will be fixed at 0.1 inch.
cax = make_axes_locatable(ax).append_axes('right', size='2%', pad=0.1)
plt.colorbar(img, cax=cax)
plt.savefig('debug_r.png', bbox_inches='tight')
```


### Visualize matrix (subplot, colorbar, save without display, tight margins, resolution, latex)

```
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

fig = plt.figure(figsize=(14, 14))
ax = fig.add_subplot(311); ax.set_title(r'$x$'); img = ax.imshow(x); plt.colorbar(img, ax=ax)
ax = fig.add_subplot(312); ax.set_title(r'$y$'); img = ax.imshow(y); plt.colorbar(img, ax=ax)
ax = fig.add_subplot(313); ax.set_title(r'$z$'); img = ax.imshow(z); plt.colorbar(img, ax=ax)
fig.savefig('debug_xyz.png', bbox_inches='tight')
```


### Unique rows of matrix

```
np.vstack({tuple(row) for row in a})
```


### Insert multiple lines

```
w, h = 5, 5
lines = [None] * (w + 1 + h + 1)
for i in range(h + 1):
	lines[i] = [(0, i), (w, i)] # [(x1, y1), (x2, y2)]
	for i in range(w + 1):
		lines[h + 1 + i] = [(i, 0), (i, h)]
lc = collections.LineCollection(lines, colors='k', linewidths=1)
ax.add_collection(lc)
ax.set_xlim((0, w))
ax.set_ylim((0, h))
ax.set_aspect('equal')
```