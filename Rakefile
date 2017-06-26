require 'http'
require 'json'

def build_node(taxon, root_taxon)
  { id: taxon["title"], group: root_taxon["title"] }
end

task :generate_network do
  root_taxons = %w(
    https://www.gov.uk/api/content/education
  )

  nodes = []
  links = []

  root_taxons.each do |taxon_url|
    root_taxon = JSON.parse(HTTP.get(taxon_url))

    nodes << build_node(root_taxon, root_taxon)

    root_taxon.dig("links", "child_taxons").to_a.each do |taxon_1|
      nodes << build_node(taxon_1, root_taxon)
      links << { source: taxon_1["title"], target: root_taxon["title"], value: 1 }

      taxon_1.dig("links", "child_taxons").to_a.each do |taxon_2|
        nodes << build_node(taxon_2, root_taxon)
        links << { source: taxon_1["title"], target: taxon_2["title"], value: 1 }

        taxon_2.dig("links", "child_taxons").to_a.each do |taxon_3|
          nodes << build_node(taxon_3, root_taxon)
          links << { source: taxon_2["title"], target: taxon_3["title"], value: 1 }

          taxon_3.dig("links", "child_taxons").to_a.each do |taxon_4|
            nodes << build_node(taxon_4, root_taxon)
            links << { source: taxon_3["title"], target: taxon_4["title"], value: 1 }

            taxon_4.dig("links", "child_taxons").to_a.each do |taxon_5|
              nodes << build_node(taxon_5, root_taxon)
              links << { source: taxon_4["title"], target: taxon_5["title"], value: 1 }
            end
          end
        end
      end
    end
  end

  File.write("network.json", JSON.pretty_generate(nodes: nodes, links: links))
end
