# Raspberry Pi cluster

An 8-node cluster built from Raspberry Pi 1 Model B+ boards, used to experiment
with distributed computing in Python using MPI (`mpi4py`).

Rank 0 is the master node; the other seven are workers.

## Files

| File | Description |
| --- | --- |
| `ping.py` | Measures round-trip ping time to each node with small messages |
| `ping_np.py` | Same as `ping.py`, but sends a large NumPy array |
| `broadcast/broadcast.py` | Broadcasts a NumPy array from the master to all nodes |
| `broadcast/array_sum.py` | Broadcasts two arrays and computes their element-wise sum |
| `broadcast/dot_product.py` | Broadcasts two arrays and computes their dot product |
| `sendRecv/sendRecv.py` | Two nodes send data to the master, which prints it |
| `sendRecv/nodeCalc.py` | Each node performs a different operation on a number passed around by the master |
| `sync` | Copies the current directory to every node with `scp` |
| `sync2` | Watches for changes and `rsync`s them to every node |

## Running

From the master node:

```bash
mpirun -np 8 --hostfile ~/hosts python3 ping.py
```

The `sync` scripts read the node list from `~/hosts` and copy to
`~/Documents/mpi` on each worker. `sync2` requires `inotifywait`.

## License

GPL-3.0. See [LICENSE.txt](LICENSE.txt).
