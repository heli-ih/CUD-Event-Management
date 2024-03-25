<script>
    import Calendar from "../lib/components/Calendar.svelte";
    export let data;
    
</script>

    
<p class="pb-5">hi <a href="/club">club</a></p>
<p class="pb-5">hi <a href="/society">society</a></p>
<p class="pb-5">hi <a href="/workshop">workshop</a></p>
<p><a href="/createEvent">create event</a></p>

<main>
    <Calendar { data }/>
</main>