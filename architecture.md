# Software Architecture
Notes for Cs121 class November 8th

## What is software architecture?

- Tends to be very abstract  
- Hard to change after you build the system
- Helps guide division of work
- Includes decision, principles, and vision

---

## Example arcitecture: Pipe and filter:


- Pipes: arrows
- filters: boxes

```           
[filter] -> [filter]  -> [filter] -> [filter] -> stream
                      \            ^
                       \>[filter] /
```
Actual example: The `|` pipe character in unix systems.                      

Good because highly reusable. Easy to mix and match many kinds of filters. 

> Unix example: `cat file | grep "search" | sed "s/.../.../" | wc -L`
 

Example using the above pipes and filters in java
```Java
import java.io.*;

class B {
    public static void main(String args[]) throws Exception {
        ProcessBuilder pb = new ProcessBuilder("ls");
        Process p = pb.start();
        p.waitFor();
        InputStream is = p.getInputStream();
        BufferReader br = new BufferReader(new InputStreamReader(is));
        
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
    }
}
```
## Example: Layered Architecture 
Things only talk to the layer directly above and below it. Abstraction.
```
[ Java program ]
[ Java Virtual machine ]
[ Operating System ]
[ Hardware ] 
```
- Java program only talks to JVM
- JVM only talks to OS and Java Program

Example 2 (Layered Architecture) : OSI Model
```
[ Application Layer {HTTP} ]
[ Presentation Layer       ]
[ Session Layer            ]
[ Transport Layer {TCP}    ]
[ Network {ip}             ] 
[ Data {ethernet}          ]
[ Physical                 ]
```

Example 3 (Layered Architecture) : Lamp Stack Web server with PHP
```
[ PHP            ]
[ MYSQL / APACHE ] (split layer)
[ LINUX          ]
```

## Example Architecture: networks
- Client / Server architectures
    - single server, single point of truth
    - trust server
- Peer to Peer
    - more scalabe
    - people talk to anyone, no single point of truth
    - less bandwidth required
