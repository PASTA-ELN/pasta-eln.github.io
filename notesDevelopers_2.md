
sudo apt install wine wine32

npm install testcafe-browser-provider-electron -s
npm install electron@latest

npm start
npm run build
sudo dpkg -i pasta-db-react-electron_0.9.0_amd64.deb


testcafe "electron:/home/sbrinckm/FZJ/PASTA/ReactElectron" "test/fixtures/*.js"