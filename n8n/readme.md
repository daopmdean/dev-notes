

setup and run on docker
```
docker volume create n8n_data
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```


Node types
1. trigger nodes
2. action nodes
3. logic nodes
4. code nodes
5. ai agent nodes

Ref
https://medium.com/data-science-collective/mastering-n8n-from-scratch-a-step-by-step-guide-for-beginners-its-easier-than-you-think-2d7ca5d47277