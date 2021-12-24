# Data-Science-Portfolio
Python Projects
class ItemToPurchase:
    def __init__(self, item_name='none', item_price=0, item_quantity=0, item_description='none'):
        self.item_name = item_name
        self.item_price = item_price
        self.item_quantity = item_quantity
        self.item_description = item_description

    def print_item_cost(self):
        string = '{} {} @ ${} = ${}'.format(self.item_name, self.item_quantity, self.item_price,
                                            (self.item_quantity * self.item_price))
        cost = self.item_quantity * self.item_price
        return string, cost

    def print_item_description(self):
        string = '{}: {}'.format(self.item_name, self.item_description)
        print(string, end=' ')
        return string

    def calc_item_cost(self):
        return self.item_quantity * self.item_price


class ShoppingCart:
    def __init__(self, customer_name='none', current_date='January 1, 2016', cart_items=None):
        if cart_items is None:
            cart_items = []
        self.customer_name = customer_name
        self.current_date = current_date
        self.cart_items = cart_items

    def add_item(self, item=ItemToPurchase):
        self.cart_items.append(item)
    
    def add(self, item=ItemToPurchase):
        print('ADD ITEM TO CART')
        item_name = str(input('Enter the item name:'))
        item_description = str(input('\nEnter the item description:'))
        item_price = int(input('\nEnter the item price:'))
        item_quantity = int(input('\nEnter the item quantity:\n'))
        self.cart_items.append(item(item_name, item_price, item_quantity, item_description))

    def remove_item(self):
        print('\nREMOVE ITEM FROM CART', end='\n')
        string = str(input('Enter name of item to remove:\n'))
        i = 0
        for item in self.cart_items:
            if (item.item_name == string):
                del self.cart_items[i]
                flag = True
                break
            else:
                flag = False
            i += 1
        if (flag == False):
            print('Item not found in cart. Nothing removed.')
    
    def modify_item(self, item=ItemToPurchase):
        print('CHANGE ITEM QUANTITY')
        item_name = str(input('Enter the item name:\n'))
        new_quantity = int(input('Enter the new quantity:\n'))
        for item in self.cart_items:
            if (item.item_name == item_name):
                item.item_quantity = new_quantity
                flag = True
            else:
                flag = False
        if (flag == False):
            print('Item not found in cart. Nothing modified.')
            
    def get_cost_of_cart(self):
        total_cost = 0

        for item in self.cart_items:
            total_cost += item.calc_item_cost()
        return total_cost

    def get_num_items_in_cart(self):
        total_quantity = 0
        for item in self.cart_items:
            total_quantity += item.item_quantity

        return total_quantity

    def print_total(self):
        tc = 0
        for item in self.cart_items:
            print('{} {} @ ${} = ${}'.format(item.item_name, item.item_quantity,
                                             item.item_price, (item.item_quantity * item.item_price)), end='\n')
            tc += (item.item_quantity * item.item_price)
        print('\nTotal: ${}'.format(tc), end='\n')
        total_cost = self.get_cost_of_cart()
        if total_cost == 0:
            print('SHOPPING CART IS EMPTY')
        else:
            print('{}\'s Shopping Cart - {}'.format(self.customer_name, self.current_date), end='\n')
            print('Number of Items:', self.get_num_items_in_cart(), end='\n\n')
            self.total_cost = self.get_cost_of_cart()()

    def print_descriptions(self):
        print('OUTPUT ITEMS\' DESCRIPTIONS')
        print('{}\'s Shopping Cart - {}'.format(self.customer_name, self.current_date), end='\n')
        print('\nItem Descriptions', end='\n')
        for item in self.cart_items:
            print('{}: {}'.format(item.item_name, item.item_description), end='\n')

    def output_cart(self):
        print('OUTPUT SHOPPING CART', end='\n')
        print('{}\'s Shopping Cart - {}'.format(self.customer_name, self.current_date), end='\n')
        print('Number of Items:', self.get_num_items_in_cart(), end='\n\n')
        self.total_cost = self.get_cost_of_cart()
        if self.total_cost == 0:
            print('SHOPPING CART IS EMPTY')
        else:
            pass
        tc = 0
        for item in self.cart_items:
            print('{} {} @ ${} = ${}'.format(item.item_name, item.item_quantity,
                                             item.item_price, (item.item_quantity * item.item_price)), end='\n')
            tc += (item.item_quantity * item.item_price)
        print('\nTotal: ${}'.format(tc), end='\n')


def print_menu():
    print("MENU")
    print("a - Add item to cart")
    print("r - Remove item from cart")
    print("c - Change item quantity")
    print("i - Output items' descriptions")
    print("o - Output shopping cart")
    print("q - Quit")

def execute_menu(option, newCart=ShoppingCart):
    customer_Cart = newCart
    if command == 'a':
        customer_Cart.add()
    if command == 'o':
        customer_Cart.output_cart()
    if command == 'i':
        customer_Cart.print_descriptions()
    if command == 'r':
        customer_Cart.remove_item()
    if command == 'c':
        customer_Cart.modify_item()
def execut_menu(*option, **new_cart):
    customer_Cart = newCart
    string = ''
    menu = ('\nMENU\n'
            'a - Add item to cart\n'
            'r - Remove item from cart\n'
            'c - Change item quantity\n'
            'i - Output items\' descriptions\n'
            'o - Output shopping cart\n'
            'q - Quit\n')
    command = ''
    while command != 'q':
        string = ''
        print('\nMENU\n'
              'a - Add item to cart\n'
              'r - Remove item from cart\n'
              'c - Change item quantity\n'
              'i - Output items\' descriptions\n'
              'o - Output shopping cart\n'
              'q - Quit\n', end='\n')
        command = input('Choose an option:')
        print()
        while command != 'a' and command != 'o' and command != 'i' and command != 'r' and command != 'c' and command != 'q':
            command = input("Choose an option:\n")
        if command == 'a':
            customer_Cart.add()
        if command == 'o':
            customer_Cart.output_cart()
        if command == 'i':
            customer_Cart.print_descriptions()
        if command == 'r':
            customer_Cart.remove_item()
        if command == 'c':
            customer_Cart.modify_item()
    else:
        command == 'q'
        exit()
    


if __name__ == "__main__":
    customer_name = str(input('Enter customer\'s name:'))
    current_date = str(input('\nEnter today\'s date:'))
    print()
    print()
    print('Customer name:', customer_name, end='\n')
    print('Today\'s date:', current_date, end='\n')
    newCart = ShoppingCart(customer_name, current_date)
    execut_menu(newCart)
