<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        :options="categories"
        label="Select a category"
        v-model="event.category"
        class="field"
      />

      <fieldset>
        <legend>
          Name & describe your event
        </legend>
        <BaseInput
          class="field"
          placeholder="Title"
          v-model="event.title"
          label="Title"
          type="text"
        />

        <BaseInput
          class="field"
          placeholder="Description"
          v-model="event.description"
          type="text"
          label="Description"
        />
      </fieldset>

      <fieldset>
      <legend>Where is your event?</legend>

      <BaseInput
        class="field"
        placeholder="Description"
        v-model="event.location"
        type="text"
        label="Location"
      />
      </fieldset>

      <fieldset>
        <legend>Pets</legend>
        <p>Are pets allowed?</p>
        <div>
          <BaseRadioGroup
            v-model="event.pets"
            name="pet"
            :options="radioButtonOptions"
          />
        </div>
      </fieldset>

      <fieldset>
        <legend>Extras</legend>
        <div>
          <BaseCheckbox
            v-model="event.extras.catering"
            class="field"
            label="Catering"
          />
        </div>

        <div>
          <BaseCheckbox
            v-model="event.extras.music"
            class="field"
            label="Live music"
          />
        </div>
      </fieldset>

      <button type="submit">Submit</button>
    </form>

    <pre>{{ event }}</pre>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  methods: {
    sendForm () {
      axios.post(
        'https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events',
        this.event
      )
        .then(function (response) {
          console.log('Response', response)
        })
        .catch(function (err) {
          console.log('Error', err)
        })
    }
  },
  data () {
    return {
      categories: [
        'sustainability',
        'nature',
        'animal welfare',
        'housing',
        'education',
        'food',
        'community'
      ],
      radioButtonOptions: [
        {
          label: 'Yes',
          value: 1
        },
        {
          label: 'No',
          value: 0
        }
      ],
      event: {
        category: '',
        title: '',
        description: '',
        location: '',
        pets: 1,
        extras: {
          catering: false,
          music: false
        }
      }
    }
  }
}
</script>

<style>
fieldset {
  border: 0;
  margin: 0;
  padding: 0;
}

legend {
  font-size: 28px;
  font-weight: 700;
  margin-top: 20px;
}
</style>
