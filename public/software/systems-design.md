# Systems Design

## What to look for in a cloud hosting solution

- If IPs are blacklisted, i.e. by the company you work for
- Encryption of sensitive data

## SSDs vs HDDs

- The traditional spinning hard drive is the basic non-volatile storage on a computer. That is, information on it doesn't "go away" when you turn off the system, unlike data stored in RAM. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=the%20traditional%20spinning%20hard%20drive%20is%20the%20basic%20non-volatile%20storage%20on%20a%20computer.%20that%20is%2C%20information%20on%20it%20doesn't%20%22go%20away%22%20when%20you%20turn%20off%20the%20system%2C%20unlike%20data%20stored%20in%20ram.))
- A hard drive is essentially a metal platter with a magnetic coating that stores your data ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=a%20hard%20drive%20is%20essentially%20a%20metal%20platter%20with%20a%20magnetic%20coating%20that%20stores%20your%20data))
- A read/write head on an arm accesses the data while the platters are spinning. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=a%20read%2Fwrite%20head%20on%20an%20arm%20accesses%20the%20data%20while%20the%20platters%20are%20spinning.))
- An SSD performs the same basic function as a hard drive, but data is instead stored on interconnected flash-memory chips that retain the data even when there's no power flowing through them. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=an%20ssd%20performs%20the%20same%20basic%20function%20as%20a%20hard%20drive%2C%20but%20data%20is%20instead%20stored%20on%20interconnected%20flash-memory%20chips%20that%20retain%20the%20data%20even%20when%20there's%20no%20power%20flowing%20through%20them.))
- SSDs are more expensive than hard drives in terms of dollar per gigabyte. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=ssds%20are%20more%20expensive%20than%20hard%20drives%20in%20terms%20of%20dollar%20per%20gigabyte.))
- Consumer SSDs are rarely found in capacities greater than 2TB, and those are expensive. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=consumer%20ssds%20are%20rarely%20found%20in%20capacities%20greater%20than%202tb%2C%20and%20those%20are%20expensive.))
- SSD vs. HDD Speed This is where SSDs shine. An SSD-equipped PC will boot in far less than a minute, often in just seconds. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=it.-,SSD%20vs.%20HDD,often%20in%20just%20seconds.,-A))
- Because hard drives rely on spinning platters, there is a limit to how small they can be manufactured. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=because%20hard%20drives%20rely%20on%20spinning%20platters%2C%20there%20is%20a%20limit%20to%20how%20small%20they%20can%20be%20manufactured.))
- SSDs have no such limitation, so they can continue to shrink as time goes on. ([source](https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=ssds%20have%20no%20such%20limitation%2C%20so%20they%20can%20continue%20to%20shrink%20as%20time%20goes%20on.%20))
- The overall takeaway? Hard drives win on price and capacity. SSDs work best if speed, ruggedness, form factor, noise, or fragmentation (technically, a subset of speed) are important factors to you. If it weren't for the price and capacity issues, SSDs would be the hands-down winner. ([source](<https://www.pcmag.com/news/ssd-vs-hdd-whats-the-difference#:~:text=the%20overall%20takeaway%3F%20hard%20drives%20win%20on%20price%20and%20capacity.%20ssds%20work%20best%20if%20speed%2C%20ruggedness%2C%20form%20factor%2C%20noise%2C%20or%20fragmentation%20(technically%2C%20a%20subset%20of%20speed)%20are%20important%20factors%20to%20you.%20if%20it%20weren't%20for%20the%20price%20and%20capacity%20issues%2C%20ssds%20would%20be%20the%20hands-down%20winner.>))

## DNS

- Typically cached, with a TTL of a few hours or a day
  - So that you don't need to do a DNS lookup for the same site over and over, unnecessarily

## Load balancing

- The load balancer can have a public IP address, and route to the individual servers, which can have private IP addresses
- Round robin
  - Downside: one user could be using one server very heavily, and now the load might be uneven. Especially since round robin will keep sending users to that server, even though it's under a heavy load.
- Need to be careful about session data, if you're using it -- don't want session data on multiple servers, that could potentially be mismatched
- Algorithms: Least connection, Least response time, Least bandwidth, Round robin, Weighted round-robin, IP hash ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=5.-,Algorithms,IP%20hash,-6))
- The smart client is a client that takes a pool of service hosts and balances load across them, detects downed hosts, and avoids sending requests their way ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=the%20smart%20client%20is%20a%20client%20that%20takes%20a%20pool%20of%20service%20hosts%20and%20balances%20load%20across%20them%2C%20detects%20downed%20hosts%2C%20and%20avoids%20sending%20requests%20their%20way))
- Hardware load balancers are specialized hardware deployed in-between the server and the client. ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=hardware%20load%20balancers%20are%20specialized%20hardware%20deployed%20in-between%20the%20server%20and%20the%20client.))
- Software load balancers generally implement a combination of one or more scheduling algorithms. ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=software%20load%20balancers%20generally%20implement%20a%20combination%20of%20one%20or%20more%20scheduling%20algorithms.))
- Most load balancer programs are also reverse proxy servers, which simplifies web application server architecture. ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=most%20load%20balancer%20programs%20are%20also%20reverse%20proxy%20servers%2C%20which%20simplifies%20web%20application%20server%20architecture.))
- It often makes sense to deploy a reverse proxy even with just one web server or application server. ([source](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27#:~:text=it%20often%20makes%20sense%20to%20deploy%20a%20reverse%20proxy%20even%20with%20just%20one%20web%20server%20or%20application%20server.))

## Scaling

- Vertical scaling has an upper limit -- you can't just keep scaling up an individual machine
- Horizontal scaling has the added benefit of adding redundancy, for better availability
- But, it's simpler to vertically scale
- Scalability is simply measured by the number of requests an application can handle successfully. Once the application can no longer handle any more simultaneous requests, it has reached its scalability limit. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=scalability%20is%20simply%20measured%20by%20the%20number%20of%20requests%20an%20application%20can%20handle%20successfully.%20once%20the%20application%20can%20no%20longer%20handle%20any%20more%20simultaneous%20requests%2C%20it%20has%20reached%20its%20scalability%20limit.))
- You can scale these resources through a combination of adjustments to network bandwidth, CPU and physical memory requirements, and hard disk adjustments. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=you%20can%20scale%20these%20resources%20through%20a%20combination%20of%20adjustments%20to%20network%20bandwidth%2C%20cpu%20and%20physical%20memory%20requirements%2C%20and%20hard%20disk%20adjustments.))
- Vertical scaling allows data to live on a single node, and scaling spreads the load through CPU and RAM resources for your machines. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=vertical%20scaling%20allows%20data%20to%20live%20on%20a%20single%20node%2C%20and%20scaling%20spreads%20the%20load%20through%20cpu%20and%20ram%20resources%20for%20your%20machines.))
- Small- and mid-sized companies most often use vertical scaling for their applications because it allows businesses to scale relatively quickly compared to using horizontal scaling. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=small-%20and%20mid-sized%20companies%20most%20often%20use%20vertical%20scaling%20for%20their%20applications%20because%20it%20allows%20businesses%20to%20scale%20relatively%20quickly%20compared%20to%20using%20horizontal%20scaling.))
- One drawback of vertical scaling is that it poses a higher risk for downtime and outages than horizontal scaling. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=one%20drawback%20of%20vertical%20scaling%20is%20that%20it%20poses%20a%20higher%20risk%20for%20downtime%20and%20outages%20than%20horizontal%20scaling.))
- Correctly provisioning your resources is the best way to ensure that upgrading was worth it and that your business will not experience the negative effects of vertical scaling. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=correctly%20provisioning%20your%20resources%20is%20the%20best%20way%20to%20ensure%20that%20upgrading%20was%20worth%20it%20and%20that%20your%20business%20will%20not%20experience%20the%20negative%20effects%20of%20vertical%20scaling.))
- Horizontal scaling means adding more machines to the resource pool, rather than simply adding resources by scaling vertically. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=horizontal%20scaling%20means%20adding%20more%20machines%20to%20the%20resource%20pool%2C%20rather%20than%20simply%20adding%20resources%20by%20scaling%20vertically.))
- Horizontal scaling is favored by DevOps experts because it is done dynamically automatically — scaling based on the load for optimal performance. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=horizontal%20scaling%20is%20favored%20by%20devops%20experts%20because%20it%20is%20done%20dynamically%20automatically%20%E2%80%94%20scaling%20based%20on%20the%20load%20for%20optimal%20performance.))
- Both vertical and horizontal scaling can be performed automatically, also known as auto-scaling, as the actual process of scaling is not particularly difficult. ([source](https://touchstonesecurity.com/horizontal-vs-vertical-scaling-what-you-need-to-know/#:~:text=both%20vertical%20and%20horizontal%20scaling%20can%20be%20performed%20automatically%2C%20also%20known%20as%20auto-scaling%2C%20as%20the%20actual%20process%20of%20scaling%20is%20not%20particularly%20difficult.))

## Caching

- Take advantage of the locality of reference principle: recently requested data is likely to be requested again. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=take%20advantage%20of%20the%20locality%20of%20reference%20principle%3A%20recently%20requested%20data%20is%20likely%20to%20be%20requested%20again.))
- Exist at all levels in architecture, but often found at the level nearest to the front end. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=exist%20at%20all%20levels%20in%20architecture%2C%20but%20often%20found%20at%20the%20level%20nearest%20to%20the%20front%20end.))
- Caching consists of 1. precalculating results (e.g. the number of visits from each referring domain for the previous day) 2. pre-generating expensive indexes (e.g. suggested stories based on a user’s click history) 3. storing copies of frequently accessed data in a faster backend (e.g. Memcache instead of PostgreSQL. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=Caching%20consists,of%20PostgreSQL.))

### Layers of caching

- 2.1 Client-side. Use case: Accelerate retrieval of web content from websites (browser or device) Tech: HTTP Cache Headers, Browsers ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2.1,Browsers))
- 2.2 DNS Use case: Domain to IP Resolution Tech: DNS Servers Solutions: Amazon Route 53 ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2.2,Route%2053))
- 2.3 Web Server Use case: Accelerate retrieval of web content from web/app servers. Manage Web Sessions (server-side) Tech: HTTP Cache Headers, CDNs, Reverse Proxies, Web Accelerators, Key/Value Stores Solutions: Amazon CloudFront, ElastiCache for Redis, ElastiCache for Memcached, Partner Solutions ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2.3,Partner%20Solutions))
- 2.4 Application Use case: Accelerate application performance and data access Tech: Key/Value data stores, Local caches Solutions: Redis, Memcached ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=Solutions-,2.4%20Application,Redis%2C%20Memcached,-Note))
  - If horizontally scaled, the nodes are going to have different caches. Which has implications WRT cache misses
  - They also might be redundantly cached, since they could be cached on different servers
  - Solutions for these ^: Global caches, distributed caches
  - If the node doesn't have something in the cache, it'll go to e.g. the database directly
- 2.5 Database Use case: Reduce latency associated with database query requests Tech: Database buffers, Key/Value data stores Solutions: The database usually includes some level of caching in a default configuration, optimized for a generic use case. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2.5,use%20case.))
- 2.6 Content Distribution Network (CDN) CDN Use case: Take the burden of serving static media off of your application servers and provide a geographic distribution. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2.6,geographic%20distribution.))

### Cache invalidation / write policies

- There are majorly three kinds of caching systems: Write-through cache, Write-around cache, Write-back cache. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=there%20are%20majorly%20three%20kinds%20of%20caching%20systems%3A%20write-through%20cache%2C%20write-around%20cache%2C%20write-back%20cache.))
- Write through cache: Where writes go through the cache and write is confirmed as success only if writes to DB and the cache BOTH succeed.
  - Pro: Fast retrieval, complete data consistency, robust to system disruptions.
  - Con: Higher latency for write operations. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=Write%20through,write%20operations.))
- Write around cache: Where write directly goes to the DB, bypassing the cache.
  - Pro: This may reduce latency.
  - Con: However, it increases cache misses because the cache system reads the information from DB in case of a cache miss. As a result, this can lead to higher read latency in the case of applications that write and re-read the information quickly. Read must happen from slower back-end storage and experience higher latency. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=Write%20around,higher%20latency.))
- Write back cache: Where the write is directly done to the caching layer and the write is confirmed as soon as the write to the cache completes. The cache then asynchronously syncs this write to the DB.
  - Pro: This would lead to a really quick write latency and high write throughput for the write-intensive applications.
  - Con: However, there is a risk of losing the data in case the caching layer dies because the only single copy of the written data is in the cache. We can improve this by having more than one replica acknowledging the write in the cache. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=latency.-,Write%20back%20cache%3A,write%20in%20the%20cache.,-4))

### Cache eviction policies

- First In First Out (FIFO): The cache evicts the first block accessed first without any regard to how often or how many times it was accessed before. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=first%20in%20first%20out%20(fifo)%3A%20the%20cache%20evicts%20the%20first%20block%20accessed%20first%20without%20any%20regard%20to%20how%20often%20or%20how%20many%20times%20it%20was%20accessed%20before.))
- Last In First Out (LIFO): The cache evicts the block accessed most recently first without any regard to how often or how many times it was accessed before. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=last%20in%20first%20out%20(lifo)%3A%20the%20cache%20evicts%20the%20block%20accessed%20most%20recently%20first%20without%20any%20regard%20to%20how%20often%20or%20how%20many%20times%20it%20was%20accessed%20before.))
- Least Recently Used (LRU): Discards the least recently used items first. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=least%20recently%20used%20(lru)%3A%20discards%20the%20least%20recently%20used%20items%20first.))
- Most Recently Used (MRU): Discards, in contrast to LRU, the most recently used items first. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=most%20recently%20used%20(mru)%3A%20discards%2C%20in%20contrast%20to%20lru%2C%20the%20most%20recently%20used%20items%20first.))
- Least Frequently Used (LFU): Counts how often an item is needed. Those that are used least often are discarded first. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=least%20frequently%20used%20(lfu)%3A%20counts%20how%20often%20an%20item%20is%20needed.%20those%20that%20are%20used%20least%20often%20are%20discarded%20first.))
- Random Replacement (RR): Randomly selects a candidate item and discards it to make space when necessary. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=random%20replacement%20(rr)%3A%20randomly%20selects%20a%20candidate%20item%20and%20discards%20it%20to%20make%20space%20when%20necessary.))

### Other

- **Global caches:** All the nodes use the same single cache space (a server or file store). Each of the application nodes queries the cache in the same way it would a local one. However, it is very easy to overwhelm a single global cache system as the number of clients and requests increase but is very effective in some architectures. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=1-,Global%20caches,effective%20in%20some%20architectures.,-Two))
- **Distributed caches:** The cache is divided up using a consistent hashing function and each of its nodes owns part of the cached data. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=2-,Distributed%20caches,of%20the%20cached%20data.,-If))
  - Pros: Cache space can be increased easily by adding more nodes to the request pool. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=pros%3A%20cache%20space%20can%20be%20increased%20easily%20by%20adding%20more%20nodes%20to%20the%20request%20pool.))
  - Cons: A missing node can lead to cache loss. We may get around this issue by storing multiple copies of the data on different nodes. ([source](https://medium.com/must-know-computer-science/system-design-caching-acbd1b02ca01#:~:text=cons%3A%20a%20missing%20node%20can%20lead%20to%20cache%20loss.%20we%20may%20get%20around%20this%20issue%20by%20storing%20multiple%20copies%20of%20the%20data%20on%20different%20nodes.))

## Redundancy and Replication

- Duplication of critical data or services with the intention of increased reliability and availability of the system. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=duplication%20of%20critical%20data%20or%20services%20with%20the%20intention%20of%20increased%20reliability%20and%20availability%20of%20the%20system.))
- Remove single points of failure and provide backups (e.g. server failover). ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=remove%20single%20points%20of%20failure%20and%20provide%20backups%20(e.g.%20server%20failover).))
- Shared-nothing architecture: Each node can operate independently of one another. No central service managing state or orchestrating activities. New servers can be added without special conditions or knowledge. No single point of failure. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Shared,failure.))
- Standby redundancy, also known as Backup Redundancy is when you have an identical secondary unit to back up the primary unit. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=standby%20redundancy%2C%20also%20known%20as%20backup%20redundancy%20is%20when%20you%20have%20an%20identical%20secondary%20unit%20to%20back%20up%20the%20primary%20unit.))
- The standby unit is not usually kept in sync with the primary unit, so it must reconcile its input and output signals on the takeover of the Device Under Control (DUC) ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=the%20standby%20unit%20is%20not%20usually%20kept%20in%20sync%20with%20the%20primary%20unit%2C%20so%20it%20must%20reconcile%20its%20input%20and%20output%20signals%20on%20the%20takeover%20of%20the%20device%20under%20control%20(duc)))
- You also need a third party to be the watchdog, which monitors the system to decide when a switchover condition is met and command the system to switch control to the standby unit and a voter. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=you%20also%20need%20a%20third%20party%20to%20be%20the%20watchdog%2C%20which%20monitors%20the%20system%20to%20decide%20when%20a%20switchover%20condition%20is%20met%20and%20command%20the%20system%20to%20switch%20control%20to%20the%20standby%20unit%20and%20a%20voter.))
- In Standby redundancy, there are two basic types, Cold Standby and Hot Standby. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=in%20standby%20redundancy%2C%20there%20are%20two%20basic%20types%2C%20cold%20standby%20and%20hot%20standby.))
- N Modular Redundancy, also known as Parallel Redundancy, refers to the approach of having multiply units running in parallel. All units are highly synchronized and receive the same input information at the same time. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Redundancy-,N%20Modular%20Redundancy%2C,at%20the%20same%20time.,-Their))
- 1:N is a design technique used where you have a single backup for multiple systems ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=1%3An%20is%20a%20design%20technique%20used%20where%20you%20have%20a%20single%20backup%20for%20multiple%20systems))
- This technique offers redundancy at a much lower cost than the other models by using one standby unit for several primary units. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=this%20technique%20offers%20redundancy%20at%20a%20much%20lower%20cost%20than%20the%20other%20models%20by%20using%20one%20standby%20unit%20for%20several%20primary%20units.))
- Database Redundancy: Have more than one copy of your data in a database system. It can be either at the table level or at the field level. Usually, the copies are called a replica. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Database%20Redundancy,a%20replica.))
- Locally Redundant Storage (LRS) LRS ensures that your data stays within a single data center in your chosen region. Data is replicated three times. LRS is cheaper than the other types of redundancy and doesn’t provide protection against data center failures. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Locally,failures.))
- Zone-Redundant Storage (ZRS) Only available for block blobs, ZRS keeps three copies of your data across two or three data centers, either within your chosen region or across two regions. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Zone,regions.))
- Geo-Redundant Storage (GRS) This is the type of redundancy that Microsoft recommends by default, and it keeps six copies of your data. Three copies stay in the primary region, and the remaining three are replicated to a secondary region. ([source](https://medium.com/must-know-computer-science/system-design-redundancy-and-replication-e9946aa335ba#:~:text=Geo,region.))

## Sharding / Partitioning

- Sharding is the practice of optimizing database management systems by separating the rows or columns of a larger database table into multiple smaller tables. ([source](https://hazelcast.com/glossary/sharding/#:~:text=sharding%20is%20the%20practice%20of%20optimizing%20database%20management%20systems%20by%20separating%20the%20rows%20or%20columns%20of%20a%20larger%20database%20table%20into%20multiple%20smaller%20tables.))
- The new tables are called “shards” (or partitions), and each new table either has the same schema but unique rows (as is the case for “horizontal sharding”) or has a schema that is a proper subset of the original table’s schema (as is the case for “vertical sharding”). ([source](https://hazelcast.com/glossary/sharding/#:~:text=the%20new%20tables%20are%20called%20%E2%80%9Cshards%E2%80%9D%20(or%20partitions)%2C%20and%20each%20new%20table%20either%20has%20the%20same%20schema%20but%20unique%20rows%20(as%20is%20the%20case%20for%20%E2%80%9Chorizontal%20sharding%E2%80%9D)%20or%20has%20a%20schema%20that%20is%20a%20proper%20subset%20of%20the%20original%20table%E2%80%99s%20schema%20(as%20is%20the%20case%20for%20%E2%80%9Cvertical%20sharding%E2%80%9D).))
- Sharding is a common concept in scalable database architectures. By sharding a larger table, you can store the new chunks of data, called logical shards, across multiple nodes to achieve horizontal scalability and improved performance. Once the logical shard is stored on another node, it is referred to as a physical shard. ([source](https://hazelcast.com/glossary/sharding/#:~:text=Sharding%20is%20a,a%20physical%20shard.))
- With massively parallel processing, you can take advantage of all the compute resources across your cluster for every query. ([source](https://hazelcast.com/glossary/sharding/#:~:text=with%20massively%20parallel%20processing%2C%20you%20can%20take%20advantage%20of%20all%20the%20compute%20resources%20across%20your%20cluster%20for%20every%20query.))
- Because the individual shards are smaller than the logical table as a whole, each machine has to scan fewer rows when responding to a query. ([source](https://hazelcast.com/glossary/sharding/#:~:text=because%20the%20individual%20shards%20are%20smaller%20than%20the%20logical%20table%20as%20a%20whole%2C%20each%20machine%20has%20to%20scan%20fewer%20rows%20when%20responding%20to%20a%20query.))
- Horizontal sharding is effective when queries tend to return a subset of rows that are often grouped together. For example, queries that filter data based on short date ranges are ideal for horizontal sharding since the date range will necessarily limit querying to only a subset of the servers. ([source](https://hazelcast.com/glossary/sharding/#:~:text=horizontal%20sharding%20is%20effective%20when%20queries%20tend%20to%20return%20a%20subset%20of%20rows%20that%20are%20often%20grouped%20together.%20for%20example%2C%20queries%20that%20filter%20data%20based%20on%20short%20date%20ranges%20are%20ideal%20for%20horizontal%20sharding%20since%20the%20date%20range%20will%20necessarily%20limit%20querying%20to%20only%20a%20subset%20of%20the%20servers.))
- Vertical sharding is effective when queries tend to return only a subset of columns of the data. For example, if some queries request only names, and others request only addresses, then the names and addresses can be sharded onto separate servers. ([source](https://hazelcast.com/glossary/sharding/#:~:text=vertical%20sharding%20is%20effective%20when%20queries%20tend%20to%20return%20only%20a%20subset%20of%20columns%20of%20the%20data.%20for%20example%2C%20if%20some%20queries%20request%20only%20names%2C%20and%20others%20request%20only%20addresses%2C%20then%20the%20names%20and%20addresses%20can%20be%20sharded%20onto%20separate%20servers.))
- Sharded databases can offer higher levels of availability. ([source](https://hazelcast.com/glossary/sharding/#:~:text=sharded%20databases%20can%20offer%20higher%20levels%20of%20availability.))
- Sharding and partitioning are both about breaking up a large data set into smaller subsets. The difference is that sharding implies the data is spread across multiple computers while partitioning does not. Partitioning is about grouping subsets of data within a single database instance. ([source](https://hazelcast.com/glossary/sharding/#:~:text=sharding%20and%20partitioning%20are%20both%20about%20breaking%20up%20a%20large%20data%20set%20into%20smaller%20subsets.%20the%20difference%20is%20that%20sharding%20implies%20the%20data%20is%20spread%20across%20multiple%20computers%20while%20partitioning%20does%20not.%20partitioning%20is%20about%20grouping%20subsets%20of%20data%20within%20a%20single%20database%20instance.))
- In many cases, the terms sharding and partitioning are even used synonymously, especially when preceded by the terms “horizontal” and “vertical.” Thus, “horizontal sharding” and “horizontal partitioning” can mean the same thing. ([source](https://hazelcast.com/glossary/sharding/#:~:text=in%20many%20cases%2C%20the%20terms%20sharding%20and%20partitioning%20are%20even%20used%20synonymously%2C%20especially%20when%20preceded%20by%20the%20terms%20%E2%80%9Chorizontal%E2%80%9D%20and%20%E2%80%9Cvertical.%E2%80%9D%20thus%2C%20%E2%80%9Chorizontal%20sharding%E2%80%9D%20and%20%E2%80%9Chorizontal%20partitioning%E2%80%9D%20can%20mean%20the%20same%20thing.))

## Notes

- A systems design interview is as much about communication with the interviewer ([source](https://blog.pragmaticengineer.com/system-design-interview-an-insiders-guide-review/#:~:text=a%20systems%20design%20interview%20is%20as%20much%20about%20communication%20with%20the%20interviewer))
- One thing you should avoid is "just memorizing" the approaches of the problems. ([source](https://blog.pragmaticengineer.com/system-design-interview-an-insiders-guide-review/#:~:text=one%20thing%20you%20should%20avoid%20is%20%22just%20memorizing%22%20the%20approaches%20of%20the%20problems.))

## Links

- [High Scalability -](http://highscalability.com/blog/category/example)
- [Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems: Kleppmann, Martin: 9781449373320: Amazon.com: Books](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321?tag=gregdoesit-20&geniuslink=true)
- [System Design Interview - An Insider's Guide](https://courses.systeminterview.com/courses/system-design-interview-an-insider-s-guide?ref=c89a35)
- [donnemartin/system-design-primer: Learn how to design large-scale systems. Prep for the system design interview. Includes Anki flashcards.](https://github.com/donnemartin/system-design-primer)