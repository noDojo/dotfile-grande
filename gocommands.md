<!-----------------------------
 ____ ____ ____ ____ ____ ____
||n |||o |||d |||o |||j |||o ||
||__|||__|||__|||__|||__|||__||
|/__\|/__\|/__\|/__\|/__\|/__\|

------------------------------->

# **Go Commands for the Terminal**

### **To fix error: File is not goimports-ed (goimports)**
-------------------------------------------------------------
- $ gofmt -w yourfile.go

### **Get/Update go module**
-------------------------------------------------------------
- $ go get github.com/username/reponame

### **Update go if it's located outside of the GOPATH**
-------------------------------------------------------------
- $ brew upgrade go

 ### **Output go env variable paths to console**
-------------------------------------------------------------
- $ go env

 ### **Find out if the function you're calling is a loop is inlined**
-------------------------------------------------------------
- $ go build -gcflags -m




# **Various Additional Notes**

### **Enable the use of go modules in GoLand**
-------------------------------------------------------------
- GoLand > Preferences > Go > Go Modules(vgo)

### **Force VS Code to reinstall its tools**
-------------------------------------------------------------
- cmd + shift + P
- Go: Install and Update Tools