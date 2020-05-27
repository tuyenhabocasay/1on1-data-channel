# 1on1-data-channel
# Step 1: install package socket.io-client
# Step 2: init socket instance in componentdidmount
socket = io('https://meetsv-staging.1on1english.vn:3001/datachannel', {
        autoConnect: true,
        secure: true
      })
socket.on('connect', () => {
        console.log('connected')
        socket.emit('join', {roomId: '<ROOM_ID>'}, res => {
          console.log(res)
        })
        socket.on('annotation', msg => {
          console.log(msg) 
        })
        
      })
socket.on('connect_error', err=>{
          console.error(err)
        })
	  
# Step 3: If you want to send message to all people in room then:

socket.emit('annotation', {roomId, data: {type: 'BACK_SLIDE'}})

# Step 4: Remove socket if componentwillunmount

socket.emit('leave', {roomId: '<ROOM_ID>'}, res=>{
	console.log(res)
})
socket.off('connect')
socket.off('join')
socket.off('connect_error')
socket.off('annotation')
socket = null;

# Note:
1. Message sent has following format:
{
  roomId: '<ROOM_ID' // always has roomId,
  data: {
  // your data here
  }
 }
2. Message recieved on event annotation is the data object like above.