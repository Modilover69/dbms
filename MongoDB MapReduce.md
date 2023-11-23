## MongoDB: MapReduce function
```
// Map function
var mapFunction = function() {
    emit(this.student, this.marks);
};

// Reduce function
var reduceFunction = function(key, values) {
    return Array.sum(values);
};

// Run the MapReduce operation
db.studentMarks.mapReduce(
    mapFunction,
    reduceFunction,
    {
        out: "studentTotalMarks" // Output collection name
    }
);
```
