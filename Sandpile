#Drop a number of sand grains, given by size, on the grid at x,y
def drop(grid,x,y,size):
    grid[y][x] += size
    
#Drop a number of sand grains, given by size at random points in the grid
def rand_drop(grid, size):
    dim = np.shape(grid)
    grid[np.random.randint(0, dim[0])][np.random.randint(0, dim[1])] += size
    
#Drops grains on sandpile and allows for collapses until all points in grid have grains < topple
def iter_sandpile(grid, drop_x, drop_y, dropsize, topple = 4, ug = 1, dg = 1, lg = 1, rg = 1):
    tot_collapse = 0
    drop(grid, drop_x, drop_y, dropsize)
    Bool = grid >= topple
    collapse = np.count_nonzero(Bool == True)
    tot_collapse += collapse
    while collapse > 0:       
        grid[Bool] -= topple

        grid[1:,:][Bool[:-1,:]] += dg
        grid[:-1,:][Bool[1:,:]] += ug
        grid[:,1:][Bool[:,:-1]] += rg
        grid[:,:-1][Bool[:,1:]] += lg

        Bool = grid >= topple
        collapse = np.count_nonzero(Bool == True)
        tot_collapse += collapse
    return tot_collapse

#Same as iter_sandpile() but uses rand_drop() instead of drop()
def iter_sandpile_rand(grid, dropsize = 1, topple = 4, ug = 1, dg = 1, lg = 1, rg = 1):
    tot_collapse = 0
    rand_drop(grid, dropsize)
    Bool = grid >= topple
    collapse = np.count_nonzero(Bool == True)
    tot_collapse += collapse
    while collapse > 0:       
        grid[Bool] -= topple

        grid[1:,:][Bool[:-1,:]] += dg #dg amount of grains transfered downwards
        grid[:-1,:][Bool[1:,:]] += ug #ug amount of grains transfered upwards
        grid[:,1:][Bool[:,:-1]] += rg #rg amount of grains transfered right
        grid[:,:-1][Bool[:,1:]] += lg #lg amount of grains transfered left

        Bool = grid >= topple
        collapse = np.count_nonzero(Bool == True)
        tot_collapse += collapse
    return tot_collapse

#Simulates the sandpile for N amount of sand drops, N given by iterations
#length, height, iterations all positive integers. Make guards to ensure this remains true
def sandpile(length, height, iterations, initial = "random",drop = "centre", dropsize = 4, topple = 4, ug = 1, dg = 1, lg = 1, rg = 1):
    if initial == "random":
        grid = np.random.randint(0, topple, (height,length))
    else:
        grid = np.zeros([height,length]) #Creating the sandpile grid
        
    if drop == "centre":
        drop= [int(np.floor(height/2)), int(np.floor(length/2))]

    n = 0
    fall = np.zeros([iterations]) #data allocation
    if drop == "random":
        while n < iterations:
            fall[n] = iter_sandpile_rand(grid, dropsize, topple = topple,  ug = ug, dg = dg, lg = lg, rg = rg)
            n += 1
    else:
        while n < iterations:
            fall[n] = iter_sandpile(grid, drop[0], drop[1], dropsize, topple, ug = ug, dg = dg, lg = lg, rg = rg)
            n += 1

    plt.pcolormesh(grid)    #colourmap of the sandpile
    plt.show                #prints the sandpile colourmap at the end of simulation    
    return grid, fall

piles = sandpile(501, 501, 10000, initial = "random", drop = "random", dropsize = 4)

#Doesn't wait for all collapses to finish before dropping. Drop, collapse, drop, collapse.
def sandpile_pour(length, height, drop_x, drop_y, drop_pour = 100000, topple = 4):
    if drop_x == "centre":
        drop_x = int(np.floor(length/2))
        
        
    if drop_y == "centre":
        drop_y = int(np.floor(height/2))
        
    grid = np.zeros([height,length])
    drop(grid,drop_x,drop_x,drop_pour)
    Bool = grid >= topple

    fall = []
    collapse = np.count_nonzero(Bool == True)
    fall.append(collapse)

    while collapse > 0:       
        grid[Bool] -= topple

        grid[1:,:][Bool[:-1,:]] += 1
        grid[:-1,:][Bool[1:,:]] += 1
        grid[:,1:][Bool[:,:-1]] += 1
        grid[:,:-1][Bool[:,1:]] += 1

        Bool = grid >= topple
        collapse = np.count_nonzero(Bool == True)
        fall.append(collapse)
        tot_collapse = 0


    plt.pcolormesh(grid)
    plt.show  
    
sandpile_pour(501, 501, "centre", "centre", drop_pour = 1000000, collapse_height = 4)
    
#turn fall array into bar chart (maybe interactive?)
plt.hist(piles[1], bins=np.logspace(0, 12, num=10, base=2), log=True)
plt.xscale("log")
plt.show()
