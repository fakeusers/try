package com.company;

public class TreeJazz {
    private Node root;
    private int treeDepth;
    private boolean flag;
    public TreeJazz(int value){
        root =new Node(value);
    }

    public void add(int value) {

        if (root==null) {
          root =new Node(value);
        }
        else {
            addRecursive(this.root, value);
        }
        treeDepth=treeDepth();
    }
    private void addRecursive(Node current, int value){

        if (value<current.value) {
            if (current.left == null) {
                current.left = new Node(value);
            } else {
                addRecursive(current.left, value);
            }
        }
        else if (value>current.value) {
            if(current.right==null){
                current.right = new Node(value);
            }
            else addRecursive(current.right,value);
        }

    }
    public int treeDepth() {
        this.treeDepth(this.root);
        return treeDepth;
    }
    private int treeDepth(Node n) {
        int leftDepth;
        int rightDepth;

        leftDepth =(n.left==null)? 0: 1+ treeDepth(n.left);
        rightDepth =(n.right==null)? 0:1+treeDepth(n.right);

        treeDepth=(leftDepth>rightDepth)? leftDepth:rightDepth;
        return treeDepth;
    }
    public boolean isPerfectTree() {
     return isPerfectTree(this.root,treeDepth,0);
    }
    private boolean isPerfectTree(Node n, int treeDepth, int currDepth){
        if(currDepth==treeDepth) {
            if (n.left==null&& n.right ==null) {
                return true;
            }
            else return false;
        }

        else if(n.left!=null && n.right !=null) {
            return isPerfectTree(n.left, treeDepth, currDepth + 1) && isPerfectTree(n.right, treeDepth, currDepth + 1);
        }
        else return false;
    }
    public void printTree() {
        printTree(this.root,0);
    }
    private void printTree( Node current, int currdepth){
    if (current.left != null) {
        printTree(current.left,currdepth+1);
        }

    this.printNode(current,currdepth);
    if(current.right != null) {
        printTree(current.right,currdepth+1);
        }
        return;
    }

    private void printNode(Node n,int currdepth) {
        for (int i = 0; i <= (this.treeDepth - currdepth); i++) {
            System.out.print("\t");
        }
        System.out.println(n.value);
        return;
    }
    public boolean isComplete(){
        this.flag = false;
        if (this.isPerfectTree()) return true;
        return isComplete(root,0);

    }



    private boolean isComplete(Node n, int depth) {

        if (n == null) return true;

        if (depth == treeDepth && n.isLeaf()) {
            System.out.println("flag up");
            flag = true;
        }

        boolean rightVal = isComplete(n.right, depth + 1);

        if (flag && depth == treeDepth - 1) {
            System.out.println("hi");
            if (n.left == null || n.right == null) {
                System.out.println("false");
                return false;
            }
        }

        boolean leftVal = isComplete(n.left, depth + 1);

        return leftVal && rightVal;

    }
}
