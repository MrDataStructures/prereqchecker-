# prereqchecker-
prerequisites checker assignment

Step 1: (THIS IS THE FIRST PART OF THE ASSIGNMENT)

AdjListInputFile name is passed through the command line as args[0]

Read from AdjListInputFile with the format:

a (int): number of courses in the graph
a lines, each with 1 course ID
b (int): number of edges in the graph
b lines, each with a source ID
Step 2:

AdjListOutputFile name is passed through the command line as args[1]

Output to AdjListOutputFile with the format:

c lines, each starting with a different course ID, then
listing all of that course's prerequisites (space separated) / import java.util.; public class AdjList { HashMap<String, ArrayList> adjacencyList; public static void main(String[] args) {

if ( args.length < 2 ) { StdOut.println("Execute: java -cp bin prereqchecker.AdjList "); return; }

// WRITE YOUR CODE HERE (THIS CREATES A HASHTABLE with an arraylist in each index. the indexes contain the courses folowed by their prereqs
StdIn.setFile(args[0]);
StdOut.setFile(args[1]);
AdjList finalList = new AdjList();
finalList.outputList();
}

public AdjList(){
    this.adjacencyList =  new HashMap<String, ArrayList<String>>();
    populateKeys();
    populateValues();
}

public void populateKeys(){
    int countCourses = StdIn.readInt();
    for(int i=0;i<countCourses;i++){
        adjacencyList.put(StdIn.readString(), new ArrayList<String>());
    } 
}

public void populateValues(){
    int preReqs = StdIn.readInt();
    for(int i=0;i<preReqs;i++){
        adjacencyList.get(StdIn.readString()).add(0, StdIn.readString());
    } 
}

public void outputList(){
    for(String course : adjacencyList.keySet()){
        StdOut.print(course);
        for(String preReqs : adjacencyList.get(course)){
            StdOut.print(" " + preReqs);
        }
        StdOut.println();
    }
    
}
}

//NEXT FILE BELOW (SECOND PART OF ASSIGNMENT) this part is to detect cycles in the graph

Step 1:

AdjListInputFile name is passed through the command line as args[0]

Read from AdjListInputFile with the format:

a (int): number of courses in the graph
a lines, each with 1 course ID
b (int): number of edges in the graph
b lines, each with a source ID
Step 2:

ValidPreReqInputFile name is passed through the command line as args[1]

Read from ValidPreReqInputFile with the format:

1 line containing the proposed advanced course
1 line containing the proposed prereq to the advanced course
Step 3:

ValidPreReqOutputFile name is passed through the command line as args[2]

Output to ValidPreReqOutputFile with the format:

1 line, containing either the word "YES" or "NO" */

public class ValidPrereq {

    private boolean checkCycle(int node, ArrayList<ArrayList<Integer>> cycle, int vis[], int dfsVis[]){
        vis[node]=1;
        dfsVis[node]=1;
        for(Integer it:cycle.get(node)){
            if(vis[it]==0){
                if(checkCycle(it, cycle, vis, dfsVis)==true){
                    return true;
                }
            }else if(dfsVis[it]==1){
                return true;
            }
        }
        dfsVis[node]=0;
        return false;
    }

    public boolean isCyclic(int N, ArrayList<ArrayList<Integer>> adj){
        int vis[] = new int[N];
        int dfsVis[] = new int[N];

        for(int i=0;i<N;i++){
            if(vis[i]==0){
                if(checkCycle(i,adj,vis,dfsVis)==true)StdOut.print("YES");
            }
        }
        StdOut.print("NO");
    }

    public static void main(String[] args) {

        if ( args.length < 3 ) {
            StdOut.println("Execute: java -cp bin prereqchecker.ValidPrereq <adjacency list INput file> <valid prereq INput file> <valid prereq OUTput file>");
            return;
        }
        // WRITE YOUR CODE HERE
        StdIn.setFile(args[0]);
        AdjList cycle = new AdjList();
        
    }
    
}
