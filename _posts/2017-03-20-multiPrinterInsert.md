##ʹ��˫��ָ��ʵ�ֵ��������insert����



������cpp
typedef struct NODE{
	int value;
	struct NODE *next;
} Node;

sll_insert(register Node **linkp, int new_valude)
{
	register Node *current;
	register Node *new;
	while((current = *linkp) != NULL && current->value < new_valude)
	{
		linkp = current->next;
	}
	
	new = (Node *)malloc(sizeof(Node));
	new-> = new_valude;
	new->next = current;
	*linkp = new;
	return true;
}
```