

Multiple factors play into the performance of NFS versions and why NFSv3 can out perform NVSv4 in certain areas.

- Network Overhead
	- NFSv4 has more overhead due to features such as atomicity, concistency which while the provide for more resiliency and consistency introduce additional network traffic.
- Cache 
	- NFSv3 has a simpler cache hierarchy than NFSv4 with fewer levels of caching. This can result in faster cache access and fewer misses.
	- NFSv3 uses a fixed 4KB block size than the variable block size in NFSv4. This can help with more responsive cache lookups.
- Multi Threading
	- NFSv3 unlike NFSv4 supports muti threading allowing for multiple client connections to be served by a single server.
- Workload Profiles
	- NFSv3 is more atuned to high performance environments where the server is I/O bound whilst NFSv4 is better tuned for I/O and CPU bound systems
- Security Improvements 
	- Advanced security options also add a layer that can reduce performance.

Some benchmark data between the versions is on the below although thats 

https://www.linux.com/news/benchmarking-nfsv3-vs-nfsv4-file-operation-performance/

NFS version Supported ONTAP version
NFSv2 ONTAP 8.2 and earlier
NFSv3 Supported in all ONTAP releases
NFSv4.0 ONTAP 8.1 and later
NFSv4.1 (with pNFS) ONTAP 8.1 and later
NFSv4.2 ONTAP 9.8 (basic protocol support)
ONTAP 9.9.1 (labeled NFS)

https://www.netapp.com/media/10720-tr-4067.pdf