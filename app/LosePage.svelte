<page>
    <stackLayout flexDirection="column">
        <label text="You lose!" textAlign="center" />
        <button on:tap={closeModal} text="Try again" class="-primary"></button>
    </stackLayout>
</page>

<style>
    stackLayout {
        padding: 30;
    }

    label {
        font-size: 30;
        text-align: center;
        color: chocolate;
    }
</style>

<script>
    import {closeModal} from 'svelte-native';
</script>