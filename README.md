#week 3 assignment in R programming
#functions enabling to cache potentially time-consuming computations

# the function makecache matrix
#a function creates a  matrix object that can cache its inverse

makeCacheMatrix <- function(x=matrix()){
  inv <- NULL
  set <- function(y){
    x <<- y
    inv <<- NULL
  }
  get <- function(){x}
  setinverse <- function(inverse) {inv <<- inverse}
  getinverse <- function() {inv}
  list(set=set, get=get, setinverse= setinverse, getinverse= getinverse)
}

#the function cachesolve 
#This function computes the inverse of the matrix returned by makeCacheMatrix  
#If the inverse has already been calculated then cacheSolve  retrieve the inverse from the cache

cacheSolve <- function(x,...){
  inv <- x$getinverse()
  if(!is.null(inv)){
    message("getting cached data")
    return(inv)
  }
  mat <- x$get()
  inv <- solve(mat, ...)
  x$setinverse(inv)
  inv
}
