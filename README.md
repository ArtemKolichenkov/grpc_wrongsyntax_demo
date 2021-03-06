# Wrong import syntax generated by grpc-tools

This demo is set up with Poetry but you could use regular virtual env, these are the demo project dependencies:
```
python = "^3.8.2"
grpcio-tools = "^1.28.1"
grpcio = "^1.28.1"
```

## The problem
When you run this command
```
poetry run python3 -m grpc_tools.protoc -I./ --python_out=./demo --grpc_python_out=./demo ./demo.proto
```
the resulting generated files `demo_pb2.py` and `demo_pb2_grpc.py` are generated without any errors.

However, `demo_pb2_grpc.py` imports `demo_pb2_grpc.py` as follows:  
`import demo_pb2 as demo__pb2`  
and I believe for python 3 it should be like this  
`from . import demo_pb2 as demo__pb2`

This causes:
- pylint(2.5.2) to indicate error
- it also breaks during runtime
  if you run python REPL here and try to import demo it will fail on that line of code with "No module named `demo_pb2`" caused in `demo_pb2_grpc.py` file.