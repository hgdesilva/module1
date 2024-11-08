<script lang="ts">
  export let id: string = '';
  const dateToday = new Date().toISOString().split('T')[0];

  let firstName: string
    let lastName: string
    let birthDate: string
    let phoneNumber: string
    let gender: string ='no select'

  const handleSubmit = (e: SubmitEvent) => {
    e.preventDefault;
    console.log({firstName, lastName, birthDate, phoneNumber, gender})


  }
</script>


<h1 class='text-2xl font-semibold mb-10'>
{#if id}
  Patient id to update is . . : {id}
{:else}
Patient create page to go here...
{/if}
</h1>

<form class='space-y-3' on:submit={e =>handleSubmit(e)}>
  <div>
    <label for='first_name' class="font-semibold block">First Name</label>
    <input bind:value={firstName} id='first_name' name='first_name' class='border p-2' type="text" required/>
  </div>

  <div>
    <label for='last_name' class="font-semibold block">Last Name</label>
    <input bind:value={lastName} id='last_name' name='last_name'class='border p-2' type="text"/>
  </div>

  <div>
    <label for='gender' class="font-semibold block">Gender</label>
    <select bind:value={gender} id='gender' class='border p-2' required>
      <option value="noselect" disabled>Please select</option>
      <option value="female">Female</option>
      <option value="male">Male</option>
      <option value="other">Other</option>    
    </select>
  </div>

    <div>
      <label for='dob' class="font-semibold block">Date of birth</label>
      <input bind:value={birthDate} id='dob' name='dob 'class='border p-2' type="date" max={dateToday} required/>
    </div>

    <div>
      <label for='phone' class="font-semibold block">Phone number</label>
      <input bind:value={phoneNumber} id='phone' name='phone' class='border p-2' type="number" min="10000" max ='999999999' required>
    </div>

    <button class="p-2 bg-black text-white mt-4">Submit</button>
  </form>


