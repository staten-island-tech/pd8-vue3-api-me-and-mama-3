<script>
let link = "https://data.cityofnewyork.us/resource/fcau-jc6k.json"
let response = await fetch(link)
let data_ = await response.json()
export let dataBIG = data_
</script>