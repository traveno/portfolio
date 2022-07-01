<script>
    import Drawer, { AppContent, Content } from '@smui/drawer';
    import List, { Item, Text } from '@smui/list';
    import Button from '@smui/button';

    let clicked = '';
</script>

<div style="z-index: 99;">
    <Button href="/">Home</Button>
    <Button href="/about">About</Button>
</div>

<Drawer>
    <Content>
        <List>
            <Item
                href="javascript:void(0)"
                on:click={() => (clicked = 'Gray Kittens')}
            >
                <Text>Gray Kittens</Text>
            </Item>
            <Item
                href="javascript:void(0)"
                on:click={() => (clicked = 'A Space Rocket')}
            >
                <Text>A Space Rocket</Text>
            </Item>
            <Item
                href="javascript:void(0)"
                on:click={() => (clicked = '100 Pounds of Gravel')}
            >
                <Text>100 Pounds of Gravel</Text>
            </Item>
            <Item
                href="javascript:void(0)"
                on:click={() => (clicked = 'All of the Shrimp')}
            >
                <Text>All of the Shrimp</Text>
            </Item>
            <Item
                href="javascript:void(0)"
                on:click={() => (clicked = 'A Planet with a Mall')}
            >
                <Text>A Planet with a Mall</Text>
            </Item>
        </List>
    </Content>
</Drawer>
 
