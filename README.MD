A demo ISO8583 server built using crate iso8583_rs (https://crates.io/crates/iso8583_rs)

Please see https://github.com/rkbalgi/iso8583_rs and https://crates.io/crates/iso8583_rs for additional documentation/reference

```
C:/Users/rkbal/.cargo/bin/cargo.exe run --color=always --package iso8583-server --bin iso8583-server
   Compiling iso8583_rs v0.1.10
   Compiling iso8583-server v0.1.0 (C:\Users\rkbal\IdeaProjects\iso8583-server)
    Finished dev [unoptimized + debuginfo] target(s) in 3.28s
     Running `target\debug\iso8583-server.exe`
current-dir: C:\Users\rkbal\IdeaProjects\iso8583-server
spec-file: .\src\sample_spec.yaml
14:09:04 [INFO] starting iso server for spec SampleSpec at port 6666
14:10:22 [DEBUG] (2) iso8583_rs::iso8583::server: Accepted new connection .. Ok(V4(127.0.0.1:52307))
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::server: reading data for mli 81 
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::server: received request: 

|31343230 f0242000 00000000 80000001| 1420.$ ......... 00000000
|00000000 00000001 00000000 31323132| ............1212 00000010
|33343536 37383931 30313030 34303030| 3456789101004000 00000020
|30303030 30303030 30313939 37373935| 0000000001997795 00000030
|38313232 3034f8f4 f0313233 34353637| 812204...1234567 00000040
|38|                                  8                00000050
                                                       00000051

 len = 0
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: computed header value for incoming message = 1420
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: parsing field : message_type
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: parsing field : bitmap
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - pan
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - proc_code
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - amount
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - stan
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - expiration_date
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - country_code
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - key_mgmt_data
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::bitmap: parsing field - reserved_data
14:10:22 [DEBUG] (3) iso8583_server: parsed incoming request - message = "1420 - Reversal" successfully. 
 : parsed message: 
 --- 
 
-Field-              : -Position-  : -Field Value- 
message_type         :             : 1420 
bitmap               :             : f02420000000000080000001000000000000000100000000 
pan                  :    002      : 123456789101 
proc_code            :    003      : 004000 
amount               :    004      : 000000000199 
stan                 :    011      : 779581 
expiration_date      :    014      : 2204 
country_code         :    019      : 840 
key_mgmt_data        :    096      : 1234 
reserved_data        :    160      : 5678  
 ----

14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 2: 123456789101
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 3: 004000
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 4: 000000000199
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 11: 779581
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 14: 2204
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 19: 840
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::iso_spec: echoing .. 96: 1234
14:10:22 [DEBUG] (3) iso8583_server: stan = 779581
14:10:22 [DEBUG] (3) iso8583_rs::iso8583::server: iso_response : 
|31343330 f0242000 02000000 00000001| 1430.$ ......... 00000000
|00000000 31323132 33343536 37383931| ....121234567891 00000010
|30313030 34303030 30303030 30303030| 0100400000000000 00000020
|30313939 37373935 38313232 3034f8f4| 01997795812204.. 00000030
|f0343030 31323334|                   .4001234         00000040
                                                       00000048
 
 parsed :
 --- 
-Field-              : -Position-  : -Field Value- 
message_type         :             : 1430 
pan                  :    002      : 123456789101 
proc_code            :    003      : 004000 
amount               :    004      : 000000000199 
stan                 :    011      : 779581 
expiration_date      :    014      : 2204 
country_code         :    019      : 840 
action_code          :    039      : 400 
key_mgmt_data        :    096      : 1234  
 --- 

14:10:22 [DEBUG] (3) iso8583_rs::iso8583::server: request processing time = 2 millis
```

You can find a Java TcpClient implementation here - https://github.com/rkbalgi/tcptester/blob/master/src/test/java/TcpClientTest.java#L39 
or a Rust TcpClient here - https://github.com/rkbalgi/iso8583_rs/blob/master/src/iso8583/test.rs#L86
