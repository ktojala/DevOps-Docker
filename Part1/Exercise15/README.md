# README

With this app you can download videos from Youtube
1. Have Docker installed in your computer from e.g. https://docs.docker.com/
2. Create a folder /gotvids into your working directory
3. Type 'docker pull ktojala/youtube-dl' on command line
4. Type 'docker run -v $(pwd):/gotvids ktojala/youtube-dl < webpage >'
5. Video appears in your /gotvids folder
