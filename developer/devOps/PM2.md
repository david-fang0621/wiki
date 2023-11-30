```jsx
# start
yarn --interpreter bash --name frontend -- start

# install
yarn global add pm2

# start
pm2 start AppName

# check
pm2 ls

# stop
pm2 stop AppName

# rename
pm2 delete AppName

# startup
pm2 startup
```
