<script lang="ts">
  
  import axios from 'axios'
  import { fhirApi } from './api'
  import type {Patient} from 'fhir/r4'
  import clsx from 'clsx'

  let page = 0

  const fetchPatients = async (page: number) => {
    const patientResponse = await fhirApi.get('Patient', {params: {
      _sort: '-_lastUpdated',
      _count: 20,
      _offset: page*20,  // _offset aka skip
    }})
    const patients = patientResponse.data
    console.log({patients})
    return patients
  }

  const formatName = (resource: Patient) => {
    const firstNameElement = resource.name?.[0]
    const firstName = firstNameElement?.given?.join(' ')
    const lastName = firstNameElement?.family

    if(lastName){
      return `${firstName} ${lastName}`
    }
  }

</script>

<p class="mb-2">
  <a class = 'p-2 bg-black text-white'  href='/patient'>Create patient</a>
</p>

<h1 class="text-2xl font-semibold">Patients on the Server</h1>

{#await fetchPatients(page)}
  Loading .....
{:then patientBundle}
  <!-- {JSON.stringify(patientBundle)} -->
  {#each patientBundle.entry as patient}
    <p class= 'py-2 hover:bg-gray-200 px-4 cursor-pointer'>
     <a href={`/patient/${patient?.resource?.id}`}> {patient?.resource?.id} : {formatName(patient?.resource)} {patient?.resource?.birthDate || ''} {patient?.resource?.gender || ''}</a>
    </p>
  {/each}
{/await}

<div class="mt-6">
  <button class={clsx("p-2 text-white", {'bg-black':page !== 0, 'bg-gray-300': page ===0})}  on:click={()=>page--} disabled={page===0}>Previous</button>
  <button class='p-2 bg-black text-white'on:click={()=>page++}>Next</button>
</div>
