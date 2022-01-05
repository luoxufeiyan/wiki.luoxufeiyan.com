# netcat

send: ` echo "hi"|nc -4u -w0 localhost 5000`

recv: `nc -lu localhost 5000`