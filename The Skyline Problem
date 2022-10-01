class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        sort(buildings.begin(), buildings.end(), [](const vector<int>& a, const vector<int>& b){return a[2] > b[2];}); // sort buildings by highest height
        vector<vector<int>> ans;
        map<int, int> points;
        for(auto i : buildings){ // set up points of interest, at most 20000
            points[i[0]] = 0;
            points[i[1]] = 0;
        }
        map<int, int> unsearched_points = points;
        unordered_map<int, int> og;

        for(auto i : buildings){ // find all points passing through POIS
            unsearched_points[i[0]] = og[i[0]]; // we may have deleted this while traversing earlier so we need to restore it for now
            auto it = unsearched_points.find(i[0]); // starting iterator
            vector<int> to_delete;
            while(it != unsearched_points.end() && it->first < i[1]){ // iterate through range l, r
                to_delete.push_back(it->first);
                it->second = max(i[2], it->second);
                points[it->first] = it->second;
                it++;
            }
            for(auto j : to_delete) { // delete searched points because they already have their max value
                og[j] = unsearched_points[j];
                unsearched_points.erase(j);
            }
        }
        int last_height = 0;
        for(auto i : points){
            int id = i.first;
            int height = i.second;
            if(height != last_height) ans.push_back({id, height}); // look for change in height
            last_height = height;
        }
        return ans;
    }
};
