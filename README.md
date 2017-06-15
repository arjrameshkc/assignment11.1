# assignment11.1


Go to the following link and click the  ‘create new app’ button. 

https://apps.twitter.com/app 

Your Access Token
This access token can be used to make API requests on your own account's behalf. Do not share your access token secret with anyone.
Access Token 173058817-wgRcN1M1V2KaIVsB7kaVtqATxG7NXbIQRkwDy1BX
Access Token Secret arorTesmpoiXiJBllaW72YZ5k3HrYlln0xlspOFoJANhE
Access Level Read and write
Owner rameshkumarc
Owner ID 173058817

Application Settings
Keep the "Consumer Secret" a secret. This key should never be human-readable in your application.
Consumer Key (API Key) 20X15AE32eOKDPfAteilNrgCE
Consumer Secret (API Secret) j1SD7MgbJ16y32hUx3cw5pma3uq5xvOEaXeikg2dgFlIhMcTvr
Access Level Read and write (modify app permissions)
Owner rameshkumarc
Owner ID 173058817 

then open terminal  and start all the deamonen, then do below command

[acadgild@localhost ~]$ jps
4896 ResourceManager
4422 NameNode
4519 DataNode
9194 Jps
5002 NodeManager
4668 SecondaryNameNode
[acadgild@localhost ~]$ sudo gedit .bashrc
[sudo] password for acadgild: 

Separte window open for edit like below

edit the export FLUME_HOME=/home/acadgild/apache-flume-1.6.0-bin and then save and close

then update by command source .bashrc

Then create source, channel and sink as below in new configuration file

TwitterAgent.sources = Twitter 
TwitterAgent.channels = MemChannel 
TwitterAgent.sinks = HDFS
  
# Describing/Configuring the source 
TwitterAgent.sources.Twitter.type = org.apache.flume.source.twitter.TwitterSource
TwitterAgent.sources.Twitter.consumerKey=20X15AE32eOKDPfAteilNrgCE
TwitterAgent.sources.Twitter.consumerSecret=j1SD7MgbJ16y32hUx3cw5pma3uq5xvOEaXeikg2dgFlIhMcTvr
TwitterAgent.sources.Twitter.accessToken=173058817-wgRcN1M1V2KaIVsB7kaVtqATxG7NXbIQRkwDy1BX
TwitterAgent.sources.Twitter.accessTokenSecret= arorTesmpoiXiJBllaW72YZ5k3HrYlln0xlspOFoJANhE
TwitterAgent.sources.Twitter.keywords=hadoop, bigdata, mapreduce, mahout, hbase, nosql
# Describing/Configuring the sink 

TwitterAgent.sources.Twitter.keywords= hadoop,election,sports, cricket,Big data

TwitterAgent.sinks.HDFS.channel=MemChannel
TwitterAgent.sinks.HDFS.type=hdfs
TwitterAgent.sinks.HDFS.hdfs.path=hdfs://localhost:9000/user/flume/tweets
TwitterAgent.sinks.HDFS.hdfs.fileType=DataStream
TwitterAgent.sinks.HDFS.hdfs.writeformat=Text
TwitterAgent.sinks.HDFS.hdfs.batchSize=1000
TwitterAgent.sinks.HDFS.hdfs.rollSize=0
TwitterAgent.sinks.HDFS.hdfs.rollCount=10000
TwitterAgent.sinks.HDFS.hdfs.rollInterval=600

TwitterAgent.channels.MemChannel.type=memory
TwitterAgent.channels.MemChannel.capacity=10000
TwitterAgent.channels.MemChannel.transactionCapacity=1000

TwitterAgent.sources.Twitter.channels = MemChannel
TwitterAgent.sinks.HDFS.channel = MemChannel

then HDFS directory in user/flume/tweets

run the flume agent  flume-ng agent -n TwitterAgent -f /home/acadgild/apache-flume-1.6.0-bin/conf/flume.conf 

then view the data using Cat commend

