<template>
  <div class="card">
    <div class="h-5rem flex flex-wrap justify-content-center card-container">
      <div
        class="flex-grow-1 flex align-items-center justify-content-center bg-blue-50 font-bold text-black m-2 px-5 py-3 border-round"
      >
        <div class="header">
          <div>Date Night Anime Recommendation</div>
        </div>
      </div>
    </div>
    <div
      class="h-30rem flex flex-wrap justify-content-center white_container card-container gap-2"
    >
      <div
        class="flex-grow-1 flex justify-content-center bg-blue-900 font-bold text-white m-2 px-5 py-3 border-round border-solid border-50"
      >
        <div>
          <div class="userName">
            User 1:
            <InputText type="text" v-model="formValues.user1" />
          </div>
          <div>
            Search:
            <MultiSelect
              v-model="selectedAnimeUser1"
              :options="animes"
              :selectionLimit="5"
              :maxSelectedLabels="2"
              optionLabel="Name"
              placeholder="Select Animes"
              :filter="true"
              class="multiselect-custom"
            >
            </MultiSelect>
          </div>
          <div class="rate">
            <template v-if="selectedAnimeLength(selectedAnimeUser1)">
              <div v-for="(n, index) in selectedAnimeUser1" :key="index">
                <div
                  class="flex flex-column md:flex-row card-container indigo-container"
                >
                  <div
                    class="flex flex-grow-1 h-auto w-16rem h-2rem bg-white-500 font-bold text-black border-round m-2"
                  >
                    {{ selectedAnimeUser1[index].Name }}
                  </div>
                  <div
                    class="flex flex-grow-1 w-8rem h-2rem bg-white-500 font-bold text-black border-round m-2"
                  >
                    <DropdownComponent
                      v-model="rating_User1[index]"
                      :options="like"
                      optionLabel="name"
                      option-value="code"
                      placeholder="Rate"
                      @change="
                        addData(
                          selectedAnimeUser1[index].Name,
                          rating_User1[index]
                        )
                      "
                    />
                  </div>
                </div></div
            ></template>
          </div>
        </div>
      </div>
      <div
        class="flex-grow-1 flex justify-content-center font-bold text-white bg-blue-900 m-2 px-5 py-3 border-round border-solid border-50"
      >
        <div>
          <div class="userName">
            User 2:
            <InputText type="text" v-model="formValues.user2" />
          </div>
          <div>
            Search:
            <MultiSelect
              v-model="selectedAnimeUser2"
              :options="animes"
              :selectionLimit="5"
              :maxSelectedLabels="2"
              optionLabel="Name"
              placeholder="Select Animes"
              :filter="true"
              class="multiselect-custom"
            >
            </MultiSelect>
          </div>
          <div class="rate">
            <template v-if="selectedAnimeLength(selectedAnimeUser2)">
              <div v-for="(n, index) in selectedAnimeUser2" :key="index">
                <div
                  class="flex flex-column md:flex-row card-container indigo-container"
                >
                  <div
                    class="flex flex-grow-1 h-auto w-16rem h-2rem font-bold text-white align-self-center border-round m-2"
                  >
                    {{ selectedAnimeUser2[index].Name }}
                  </div>
                  <div
                    class="flex flex-grow-1 w-8rem h-2rem bg-white-500 font-bold text-black border-round m-2"
                  >
                    <DropdownComponent
                      v-model="rating_User2[index]"
                      :options="like"
                      optionLabel="name"
                      option-value="code"
                      placeholder="Rate"
                      @change="
                        addData(
                          selectedAnimeUser2[index].Name,
                          rating_User2[index]
                        )
                      "
                    />
                  </div>
                </div></div
            ></template>
          </div>
        </div>
      </div>
    </div>
    <div
      class="flex flex-wrap justify-content-center card-container blue-container"
    >
      <div
        class="flex-grow-1 flex align-items-center justify-content-center bg-blue-800 font-bold text-xs font-light text-white m-2 px-5 py-3 border-round"
      >
        <ButtonComponent
          label="Get Recommendation"
          @click="recommender(user_anime_data)"
        ></ButtonComponent>
      </div>
    </div>
    <div
      class="h-26rem flex flex-wrap justify-content-center card-container blue-container"
    >
      <div
        class="flex-grow-1 flex bg-blue-800 text-center text-white m-2 px-5 py-3 border-round"
      >
        <template v-if="displayTable()">
          <table>
            <tr>
              <th>Anime Name</th>
              <th>Synopsis</th>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[0]["animeName"] }}</td>
              <td>{{ generatedRecommendations[0]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[1]["animeName"] }}</td>
              <td>{{ generatedRecommendations[1]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[2]["animeName"] }}</td>
              <td>{{ generatedRecommendations[2]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[3]["animeName"] }}</td>
              <td>{{ generatedRecommendations[3]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[4]["animeName"] }}</td>
              <td>{{ generatedRecommendations[4]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[5]["animeName"] }}</td>
              <td>{{ generatedRecommendations[5]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[6]["animeName"] }}</td>
              <td>{{ generatedRecommendations[6]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[7]["animeName"] }}</td>
              <td>{{ generatedRecommendations[7]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[8]["animeName"] }}</td>
              <td>{{ generatedRecommendations[8]["synopsis"] }}</td>
            </tr>
            <tr>
              <td>{{ generatedRecommendations[9]["animeName"] }}</td>
              <td>{{ generatedRecommendations[9]["synopsis"] }}</td>
            </tr>
          </table></template
        >
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import axios from "axios";
import AnimeSynopsis from "@/interface/AnimeSynopsis";
import Anime from "@/interface/Anime";
import Rating from "@/interface/Rating";

export default defineComponent({
  setup() {
    const selectedAnimeUser1 = ref<Anime[]>([]);
    const selectedAnimeUser2 = ref<Anime[]>([]);
    const user_anime_data = ref<Rating[]>([]);
    const rating_User1 = ref<Rating[]>([]);
    const rating_User2 = ref<Rating[]>([]);
    const generatedRecommendations = ref<AnimeSynopsis[]>();
    const formValues = {
      user1: "",
      user2: "",
    };
    const animes = ref<Anime[]>([]);

    const addData = (animeName: string, rating: number) => {
      const data = { animeName, rating };
      user_anime_data.value.push(data);
    };

    const like = ref([
      { name: "5/Average", code: "5" },
      { name: "6/Fine", code: "6" },
      { name: "7/Good", code: "7" },
      { name: "8/Very Good", code: "8" },
      { name: "9/Great", code: "9" },
      { name: "10/Masterpiece", code: "10" },
    ]);

    const animeOption = async () => {
      const url = `http://127.0.0.1:5555/api/animes`;

      try {
        const { data } = await axios.get(url);
        animes.value = data;
      } catch (error: any) {
        console.error(error.response);
      }
    };

    const selectedAnimeLength = (selectedAnime: any) => {
      if (selectedAnime.length === 5) return true;
    };

    const displayTable = () => {
      if (generatedRecommendations.value) return true;
    };

    const recommender = async (request: Rating[]) => {
      const url = "http://127.0.0.1:5555/api/recommendations";

      try {
        const { data } = await axios.post(url, request);
        generatedRecommendations.value = data;
      } catch (error: any) {
        console.error(error.response);
      }
    };

    animeOption();

    return {
      formValues,
      animes,
      animeOption,
      selectedAnimeUser1,
      selectedAnimeUser2,
      like,
      addData,
      user_anime_data,
      selectedAnimeLength,
      rating_User1,
      rating_User2,
      recommender,
      generatedRecommendations,
      displayTable,
    };
  },
});
</script>

<style>
body {
  background-image: url("@/assets/background.jpeg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
.rate {
  padding-top: 25px;
}
.p-button {
  background-color: white;
}
.p-button-label {
  color: black;
  font-weight: 500;
}
.userName {
  padding-bottom: 15px;
  font-size: 1.3em;
}
.p-multiselect {
  width: 18rem;
}

::v-deep(.multiselect-custom) {
  .p-multiselect-label:not(.p-placeholder) {
    padding-top: 0.25rem;
    padding-bottom: 0.25rem;
  }

  .anime-item-value {
    padding: 0.25rem 0.5rem;
    border-radius: 3px;
    display: inline-flex;
    margin-right: 0.5rem;
    background-color: var(--primary-color);
    color: var(--primary-color-text);
  }
}

.p-multiselect-items {
  max-width: 300px;
}
.p-multiselect-item {
  color: black;
  font-size: 0.875em;
  inline-size: 500px;
  overflow-wrap: break-word;
}
.note {
  font-size: 0.7em;
}
.header {
  font-size: 1.35em;
}
table,
td,
th {
  border: 1px solid;
  padding: 1px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 15px;
}
</style>
