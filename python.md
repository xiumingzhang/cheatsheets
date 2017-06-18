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


### Visualize matrix (single plot, colorbar, save without display, tight margins, resolution)

```
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

plt.figure(figsize=(14, 14))
plt.imshow(r)
plt.colorbar()
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