# WebRTC

WebRTC is used to make peer to peer connection between browsers.

## Difference between WebSocket and WetRTC

Both can be used for real time communication.

In websockets server is responsible for making real time communication, suppose there are two clients C1 and C2, if user C1 wants to send some message to other users, first C1 message reaches to server and then there was some required process done required and then it emit the event to all the users to make changes so user can get it real time.

Websockets based on TCP protocol, that means they always focus on reliable data transfer no data loss. So it is used for chat application because no message loss.

While WebRTC focuses on real-time audio, video streaming and video conferencing applications, WebSocket is primarily geared towards data communication, collaborative environments and real-time chat applications.

WebRTC is based on UDP protocol, that means they does not focus on reliable data transfer there was some loss in data transfer, because in video calling if some frames loss it is ok, but it want's to be real time.

If we are using webrtc so we can even bypass server connection.

If webrtc helps clients to directly connects than how it actually works.
- Whenever any piece of information send through wertc this process is known as `signalling`.
- For both the client to actually know each other we need to setup a mechanism sometimes we use own server, to client know each other using some id like IP address.
- `ICE Server` Interactive Connectivity Establishment (ICE) is a standard for using STUN and TURN to establish connectivity between two endpoints. ICE takes all of the complexity implied in the discussion above, and coordinates the management of STUN, TURN, and TURNS to 
    - a) optimize the likelihood of connection establishment, and 
    - b) ensure that precedence is given to preferred network communication protocols.

- `STUN Server` Session Traversal Utilities for NAT (STUN) - Used to establish a direct UDP connection between two clients.
- `TURN Server` Traversal Using Relay around NAT (TURN) - Used to establish a relayed UDP or TCP connection between two clients. Here, the traffic must be relayed through the TURN server to bypass restrictive firewall rules, and the preference is UDP over TCP because TCP's guaranteed ordered delivery of packets implies overhead that is undesirable for real-time communications. 
- `TURNS Server` Secure Traversal Using Relay around NAT (TURNS) - Used to establish a relayed TCP/TLS connection between two clients. Here, the traffic must be relayed through the TURN server and through a TLS socket to bypass extremely restrictive firewall rules.
- `NAT` Network Address Translation (NAT): To access the Internet, one public IP address is needed, but we can use a private IP address in our private network. The idea of NAT is to allow multiple devices to access the Internet through a single public address. To achieve this, the translation of a private IP address to a public IP address is required. Network Address Translation (NAT) is a process in which one or more local IP address is translated into one or more Global IP address and vice versa in order to provide Internet access to the local hosts. 

- A turn server in webrtc communiction is used to relay data betweeb peers. When a direct communication is not possible.

![TURN/STUN architecture](./images/turn.jpeg "turn server")
Real Time Transport Proctocol(RTP)

- We don't want to write turn servers with own there is already prepared turn turn srevers.
[List of available turn servers](https://gist.github.com/sagivo/3a4b2f2c7ac6e1b5267c2f1f59ac6c6b)

- SDP (Session Description Protocol): SDP (Session Description Protocol) is the standard describing a peer-to-peer connection. SDP contains the codec, source address, and timing information of audio and video.

    ```
    Here is a typical SDP message:

    v=0
    o=alice 2890844526 2890844526 IN IP4 host.anywhere.com
    s=
    c=IN IP4 host.anywhere.com
    t=0 0
    m=audio 49170 RTP/AVP 0
    a=rtpmap:0 PCMU/8000
    m=video 51372 RTP/AVP 31
    a=rtpmap:31 H261/90000
    m=video 53000 RTP/AVP 32
    a=rtpmap:32 MPV/90000
    ```

    SDP is never used alone, but by protocols like RTP and RTSP. SDP is also a component of WebRTC, which uses SDP as a way of describing a session.