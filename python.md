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


### Visualize matrix (subplot, colorbar, save without display, tight margins)

```
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

fig = plt.figure(figsize=(14, 14))
ax = fig.add_subplot(311); img = ax.imshow(x / r); plt.colorbar(img, ax=ax)
ax = fig.add_subplot(312); img = ax.imshow(y / r); plt.colorbar(img, ax=ax)
ax = fig.add_subplot(313); img = ax.imshow(z / r); plt.colorbar(img, ax=ax)
fig.savefig('debug_xyz.png', bbox_inches='tight')
```