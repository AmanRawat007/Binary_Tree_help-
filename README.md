# Binary_Tree_help-

#include <bits/stdc++.h>
using namespace std;
struct node
{
    int key;
    struct node *left, *right;
};

struct node *newNode(int item)
{
    struct node *temp =  (struct node *)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

struct node* insert(struct node* node, int key)
{
    if (node == NULL)  return newNode(key);
    if (key < node->key)
        node->left  = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);   
    return node;
}

void inorder(struct node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d \n", root->key);
        inorder(root->right);
    }
}

int height(struct node* node) 
{
    if (node==NULL)  return 0;
    else
    {
        int lDepth = height(node->left);
        int rDepth = height(node->right);
        return max(lDepth,rDepth)+1;
    }
}

void levelorder(node *node)
{
    queue<struct node*> q;
    q.push(node);
    while(!q.empty())
    {
        cout<<q.front()->key<<" ";
        if(q.front()->left!=NULL)  q.push(q.front()->left);
        if(q.front()->right!=NULL) q.push(q.front()->right);
        q.pop();
    }
}

int main()
{
    struct node *root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 60);
    inorder(root);
    cout<<"height :- "<<height(root)<<endl;
    cout<<"Level order traversal :- ";
    levelorder(root);
    return 0;
}
